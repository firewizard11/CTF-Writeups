# TShark Challenge I: Teamwork

## Situation

> An alert has been triggered: "The threat research team discovered a suspicious domain that could be a potential threat to the organisation."

We are given a packet capture file `teamwork.pcap` to analyze. We can use VirusTotal and TShark.

Ok so from this we can gather that we are looking for a suspicious domain and we need to get information about it.

## Writeup

### Task 1: What is the full URL of the malicious/suspicious domain address?

Note: It needs to be defanged for the submission

Using tshark we can extract the hosts found in the pcap using the command: `tshark -r teamwork.pcap -z hosts -q`
- -z hosts returns the resolved ip and domains in the pcap
- -q will just show the stats instead of also the packets

```text
184.154.127.226	[REDACTED]
172.217.7.228	toolbarqueries.l.google.com
216.58.217.100	toolbarqueries.l.google.com
2607:f8b0:4004:800::2004	toolbarqueries.l.google.com
```
The suspicious domain is definitely `[REDACTED]`

So we just need to defang the full URL to submit which gives us `[REDACTED]`

### Task 2: When was the URL of the malicious/suspicious domain address first submitted to VirusTotal?

Navigating to virustotal.com and pasting the **FULL URL** shows us a bunch of information about this item but we want to know the first submission which is under Details -> History and we see that the first submission was on `[REDACTED]`

### Task 3: Which known service was the domain trying to impersonate?

Based on the domain we can confirm that the domain is trying to impersonate `PayPal`

### Task 4: What is the IP address of the malicious domain? (Defanged)

From our tshark results we can find the IP of the domain. To defang it we just add brackets around the dots (\[.]) to get `[REDACTED]`

### Task 5: What is the email address that was used?

I didn't really know where to look so first I ran `tshark -r teamwork.pcap -Y "http.host == www.paypal.com4uswebappsresetaccountrecovery.timeseaways.com"` to see what requests where made and one path stood out to meat `/inc/login.php` so I narrowed down to that frame by extending my previous command with `-Y "http.host ... && frame.number eq 202"-T fields -e http.file_data` which will dump the body of the request which returned

```text
user=[REDACTED]&pass=johnny5alive&xBrowser=Mozilla+FireFox+v43&xOperatingSystem=Linux&xPlatForm=Desktop+Platform&xTimeZone=Mon+Apr+17+2017+22%3A00%3A35+GMT-0400+(EDT)&xResoLution=Computer%3A+1920x1080%3B+Browser+inner%3A+1920x762%3B+Browser+outer%3A+1920x1027&xLang=en-US
```

We can see in the user field what looks like an email `[REDACTED]` which we first need to URL decode and defang to get `[REDACTED]` which provides us the answer.


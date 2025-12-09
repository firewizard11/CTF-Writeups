# runme.py

**Challenge Link:** <https://play.picoctf.org/practice/challenge/250>

## Description

>Run the runme.py script to get the flag. Download the script with your browser or with wget in the webshell.

## Writeup

First I downloaded the script using `wget`.

```sh
wsl@PC01:/tmp/ctf$ wget https://artifacts.picoctf.net/c/34/runme.py
--2025-12-09 16:23:05--  https://artifacts.picoctf.net/c/34/runme.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 13.224.181.9, 13.224.181.40, 13.224.181.76, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|13.224.181.9|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 270 [application/octet-stream]
Saving to: ‘runme.py’

runme.py                      100%[=================================================>]     270  --.-KB/s    in 0s

2025-12-09 16:23:06 (63.7 MB/s) - ‘runme.py’ saved [270/270]
```

Then I read the file using `cat` to make sure it's not some crazy virus.

```sh
wsl@PC01:/tmp/ctf$ cat runme.py
#!/usr/bin/python3
################################################################################
# Python script which just prints the flag
################################################################################

flag ='>> FLAG WAS HERE <<'
print(flag)
```

But because of how the file is written we can just run it like a normal program on linux using `./runme.py`.

If that doesn't work you might not have execute permissions on the file which you can fix by using `chmod +x runme.py`

After it's run we get the flag!!!

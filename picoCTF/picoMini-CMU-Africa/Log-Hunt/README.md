# Log Hunt

**Challenge Link:** <https://play.picoctf.org/practice/challenge/527>

## Description

> Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag?

## Writeup

After downloading `server.log` I took a look at the first couples and noticed this line.

> [1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_

Then I did a search through the file for `FLAGPART` to confirm that all the lines with flag parts contain a part of the flag but also some of them repeat.

Using this information I wrote the following python script to go through the log and recreate the flag.

```py
with open("server.log", "r") as srvlog:
    flag_parts = []
    
    for line in srvlog:
        if "FLAGPART" in line:
            flag_part = line.split()[-1]
            
            if not (flag_part in flag_parts):
                flag_parts.append(flag_part)

    print("".join(flag_parts))
```

Does this count as using my linux skills??

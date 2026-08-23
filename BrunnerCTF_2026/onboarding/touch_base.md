# Touch Base

## Writeup

The description is really heavily is pointing us to decode the (base64 looking) string in CyberChef. So I decided to use the command `base64 -d msg` where `msg` is a file containing the encoded message. Doing so gave me the flag!!!

```text
┌──(kali㉿kali)-[~]
└─$ echo "YnJ1bm5lcnt0MHVjaDFuZ19iNHMzNjRfMTVfaDMxMTRfYjQ1M2QhfQ==" > msg
                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ base64 -d msg 
brunner{[REDACTED]}                                                                                                                       
```

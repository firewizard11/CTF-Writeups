# Bears

## Writeup

For this challenge we are given a file `bear.png`. After confirming the file is a png

```text
┌──(kali㉿kali)-[/tmp/ctf/misc_bears]
└─$ file bear.png 
bear.png: PNG image data, 800 x 600, 8-bit/color RGB, non-interlaced
```

I ran `exiftool` to check if any hints are in the metadata which happened to have the flag in it. (I was thinking the desc hinted at stego but nope).

```text
┌──(kali㉿kali)-[/tmp/ctf/misc_bears]
└─$ exiftool bear.png                                           
ExifTool Version Number         : 13.55
File Name                       : bear.png
Directory                       : .
File Size                       : 39 kB
File Modification Date/Time     : 2026:08:14 16:46:24+10:00
File Access Date/Time           : 2026:08:23 15:02:06+10:00
File Inode Change Date/Time     : 2026:08:23 15:00:50+10:00
File Permissions                : -rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 800
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Comment                         : brunner{REDACTED}
Image Size                      : 800x600
Megapixels                      : 0.480
```

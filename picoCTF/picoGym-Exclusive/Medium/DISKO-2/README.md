# DISKO 2

**Challenge Link:** <https://play.picoctf.org/practice/challenge/506?difficulty=2&originalEvent=gym&page=1&solved=1>

## Description

> Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!

## Writeup

### Initial Analysis

After downloading and unzipping the disk image `disko-2.dd` I ran `chmod -w disko-2.dd` to avoid accidently making changes to the file.

Now that we have the file ready I'm going to start getting a picture of the disk image layout using `mmls`.

```sh
wsl@win10:/tmp/ctf$ mmls disko-2.dd
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000053247   0000051200   Linux (0x83)
003:  000:001   0000053248   0000118783   0000065536   Win95 FAT32 (0x0b)
004:  -------   0000118784   0000204799   0000086016   Unallocated
```

We can see that the there is a linux partition so now we can try and fine the flag in this parititon.

### Linux Partition Analysis

For this stage I ran `mmcat disko-2.dd 2 > lin_fs` to extract the linux partition to it's own file.

Using this file I can run `strings lin_fs` to get the strings and pipe it to `grep picoCTF` to see if any flags show up.

```sh
wsl@win10:/tmp/ctf$ strings lin_fs | grep picoCTF
>> FLAG WAS HERE <<
```

And we got the flag!!!

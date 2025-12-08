# DISKO 3

**Challenge Link:** <https://play.picoctf.org/practice/challenge/507?difficulty=2&originalEvent=gym&page=1&solved=1>

## Description

> Can you find the flag in this disk image? This time, its not as plain as you think it is!

## Writeup

After downloading the disk image I ran `chmod -w disko-3.dd` to avoid making changes to the file.

### Initial Analysis

I tried running various **Volume Level** Sleuthkit tools but got 0 output for all of them.

Next I tried running `fsstat disko-3.dd` which showed that the disk image is just a **single fat32 parititon**.

```sh
wsl@win10:/tmp/ctf$ fsstat disko-3.dd
FILE SYSTEM INFORMATION
--------------------------------------------
File System Type: FAT32

OEM Name: mkfs.fat
Volume ID: 0x49838d0b
Volume Label (Boot Sector): NO NAME
Volume Label (Root Directory):
File System Type Label: FAT32
Next Free Sector (FS Info): 36434
Free Sector Count (FS Info): 1375

Sectors before file system: 0

File System Layout (in sectors)
Total Range: 0 - 204799
* Reserved: 0 - 31
** Boot Sector: 0
** FS Info Sector: 1
** Backup Boot Sector: 6
* FAT 0: 32 - 1607
* FAT 1: 1608 - 3183
* Data Area: 3184 - 204799
** Cluster Area: 3184 - 204799
*** Root Directory: 3184 - 3184
```

### Filesystem Analysis

For this stage I ran `fls` on the disk image too see if any filename structures are present and if anything stands out.

```sh
wsl@win10:/tmp/ctf$ fls disko-3.dd
d/d 4:  log
v/v 3225859:    $MBR
v/v 3225860:    $FAT1
v/v 3225861:    $FAT2
V/V 3225862:    $OrphanFiles
```

`log` is pretty interesting to see amongst all of these filesystem stuctures so I ran `fls disko-3.dd 4` to look inside the log directory and found something else that's interesting.

```sh
r/r 522628:     flag.gz
```

There is a zipped file called `flag`???

### Extracting the flag

To extract the flag we can use `icat` and since we have the **inode number** for the file we can simply output the data to a local file like so.

```sh
wsl@win10:/tmp/ctf$ icat disko-3.dd 522628 > flag.gz
wsl@win10:/tmp/ctf$ file flag.gz
flag.gz: gzip compressed data, was "flag", last modified: Thu Jul 17 15:06:53 2025, from Unix, original size modulo 2^32 53
```

From the `file` output we can see that it recognizes the file as a gzip file and now we can try and unzip the file to get the flag.

```sh
wsl@win10:/tmp/ctf$ gunzip flag.gz
wsl@win10:/tmp/ctf$ ls
disko-3.dd  flag
wsl@win10:/tmp/ctf$ cat flag
Here is your flag
>>> FLAG WAS HERE <<<
```

Now we have the flag!!!

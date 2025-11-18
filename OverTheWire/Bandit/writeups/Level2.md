# Level 2

## Level Goal

> The password for the next level is stored in a file called - located in the home directory

## Writeup

Continuing from Level 1 I listed the files again and the name of the file was actually just the dash character.

```sh
bandit1@bandit:~$ ls
-
```

We can't just use `cat -` because `-` is interpreted in a special way.

```sh
bandit1@bandit:~$ cat -
^C
bandit1@bandit:~$ 
```

So to read the file `-` we need to use a different format to specify our path. In this case I'm going to use `cat ./-` where `./` is the current folder.

And now we have the password!!

```sh
bandit1@bandit:~$ cat ./-
***************************
```

Using this password we just need to log back in to `bandit2` using the same ssh commands from before.

```sh
┌──(kali㉿kali)-[~]
└─$ ssh bandit2@bandit.labs.overthewire.org -p 2220
```
```text
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-1
bandit2@bandit.labs.overthewire.org's password: 
```

```sh
bandit2@bandit:~$ whoami
bandit2
```

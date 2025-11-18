# Level 3

## Level Goal

> The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

## Writeup

Similar to the last challenge we have a file with characters in the name that interact unexpectedly with the command line.

In this case spaces signify the end of an argument for the command. For example for `cat`: `cat spaces in this file` would show the contents of the files spaces, in, this and file.

So to read the contents of this page we need to **escape** the space characters using the `\` character like `cat spaces\ in\ this\ filename` and combined with what we saw last level we can get the dashes too so the final command is `cat ./--spaces\ in\ this\ filename--`

```sh
bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename--
******************************
```

Now that we have the password we can login to the next level.

```sh
┌──(kali㉿kali)-[~]
└─$ ssh bandit3@bandit.labs.overthewire.org -p 2220
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
bandit3@bandit.labs.overthewire.org's password: 
```
```sh
bandit3@bandit:~$ whoami
bandit3
```

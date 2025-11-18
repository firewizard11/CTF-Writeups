# Level 1

## Level Goal

> The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## Writeup

Continuing from Level 0 I used the command `ls` to list the files in this directory which had `readme` present.

```sh
bandit0@bandit:~$ ls
```
```text
readme
```

Then using `cat` I opened the contents of the file which had the password at the end.

```sh
bandit0@bandit:~$ cat readme
```
```text
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: **************************
```

Then I need to logout of bandit0 and login back into the server using the credentials for bandit1 using the command `ssh bandit1@bandit.labs.overthewire.org -p 2220` and the password I found above.

```sh
bandit0@bandit:~$ exit
```
```text
logout
Connection to bandit.labs.overthewire.org closed.
```

```sh
┌──(kali㉿kali)-[~]
└─$ ssh bandit1@bandit.labs.overthewire.org -p 2220
```
```sh
bandit1@bandit:~$ whoami
bandit1
```

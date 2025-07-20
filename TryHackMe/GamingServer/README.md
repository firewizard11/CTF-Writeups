# GamingServer

## Description

> Can you gain access to this gaming server built by amateurs with no experience of web development and take advantage of the deployment system.

## Writeup

### Port Scan

Starting off I ran a **rustscan** port scan over the whole port range using the command `rustscan -a $IP -r 1-65535 --ulimit 5000 -g`. From this I got `10.10.15.141 -> [22,80]`.

Now I can put those numbers through **nmap** to do a more targetted scan.

```text
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 340efe0612673ea4ebab7ac4816dfea9 (RSA)
|   256 49611ef4526e7b2998db302d16edf48b (ECDSA)
|_  256 b860c45bb7b2d023a0c756595c631ec4 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
| http-methods: 
|_  Supported Methods: POST OPTIONS HEAD GET
|_http-title: House of danak
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Pretty basic results with no good vulnerabilities so I'm going to check out the webserver.

### HTTP

![Homepage](images/homepage.png)

The site had a pretty cool look with a couple pages linked on the homepage. Of these pages one stoodout `http://10.10.15.141/about.html`.

![About Page](images/about.png).

You might notice the giant green **Uploads** button. Clicking this shows us the `/uploads/` directory list which had some interesting files

![Uploads Directory](images/uploads.png)

The one that stands out is `dict.lst` which is a password list which we can use to bruteforce a login. I noticed I didn't have a username so I looked back through the site and found the following comment.

![Comment](images/comment.png)

### SSH Attempt 1

Using the username `john`, I'm going to bruteforce the ssh password using **hydra** and `dict.lst`.

**Command**: `hydra -l john -P dict.lst ssh://$IP`

### HTTP Again

This actually didn't give me any success so I went back to http and moved onto some content discovery. First off I ran a directory scan using **feroxbuster**.

**Command**: `feroxbuster --url http://$IP/ --wordlist=/usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-big.txt -t 200`

From this I found an RSA Private key at `http://10.10.15.141/secret/secretKey`.

### Initial Access (SSH)

Of course I tried to login into `john` using SSH with that key but it has a passphrase (Note: don't forget to `chmod 600 secretKey`).

Now I'm going to use **JohnTheRipper** to hopefully get the passphrase. First off I need to convert the private key to a john format using `ssh2john.py secretKey > hash.txt`. Next I just ran `john hash.txt` which gave me the passphrase.

![SSH Passphrase](images/passphrase.png)

**BOOM!!!** Now we have initial access to the account `john` using ssh.

![SSH Login](images/ssh.png)

`user.txt` can be found in `john`'s home directory.

### Privilage Escalalation

PLACEHOLDER

# logon

## Description

The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at?

## Approach

Navigating to the link takes us to a logon page

![Landing Page](images/landing.png)

I tried loggin in as `joe` with the password `123` and it was successful??

![Success?](images/success.png)

I went back and tried logging in as `Joe` with the same password and it Failed so I guess Joe was the right username.

![Failed](images/Failed.png)

I went back to the successful one to see what the cookie situation was with a successful login and found out that we get some interesting cookies like `admin`, `password` and `username`.

Since admin was set to false and it's ADMIN I decided to set it to `True` so see what happens.

![Cookies](images/cookies.png)

Reloading the page gave us a flag!!

![Flag](images/flag.png)

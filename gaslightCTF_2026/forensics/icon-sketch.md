# icon-sketch

## Room Info

- Points: 488
- Author: riyc
- Attachments: `icon.zip`

## Writeup

### Initial Analysis

For this one I started with `file` which didnt show anything suspicious. Next I ran exiftool which had some interesting results.

```text
...
Document Name                   : dGhlIHBlZSBwZW9wbGUgc2FpZCB0byBkZWNvZGUgYW5kIHB1dCB0aGUgdGl0bGVzIHRvZ2V0aGVy
...
Artwork Title                   : MmUgMmUgMmUgMmUgMmUgMmUgMmUgMmUgNDMgNTQgNDYgMmUgMmUgMmUgNWYgMmUgNjggMzQgMmUgNWYgMmUgMmUgNzAgNzAgMzAgNzMgMzMgMmUgMmUgMzIgNjIgNWYgMmUgMzEgNzMgMmUgMmUgN2Q=
Title                           : dHpob3J0c2cuLi57cjUuZy4uZy5oZi4uLi4ud18uLi5rLi5oPy4=
...
```

### Weird Metadata

So some of the metadata fields contain base64 values.

```text
dGhlIHBlZSBwZW9wbGUgc2FpZCB0byBkZWNvZGUgYW5kIHB1dCB0aGUgdGl0bGVzIHRvZ2V0aGVy -> the pee people said to decode and put the titles together

MmUgMmUgMmUgMmUgMmUgMmUgMmUgMmUgNDMgNTQgNDYgMmUgMmUgMmUgNWYgMmUgNjggMzQgMmUgNWYgMmUgMmUgNzAgNzAgMzAgNzMgMzMgMmUgMmUgMzIgNjIgNWYgMmUgMzEgNzMgMmUgMmUgN2Q= -> ........CTF..._.h4._..pp0s3..2b_.1s..}

dHpob3J0c2cuLi57cjUuZy4uZy5oZi4uLi4ud18uLi5rLi5oPy4= -> gaslight...{i5.t..t.su.....d_...p..s?.
```

(btw it wasn't just base64 decode except for the first message)

### Finding the flag

So now putting the pieces together gives us `gaslightCTF{[REDACTED]}` (weird piss thing tho).

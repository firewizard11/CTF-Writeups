# Flag in Flame

**Challenge Link:** <https://play.picoctf.org/practice/challenge/523>

## Description

>The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log.

## Writeup

After downloading `log.txt` I tried running `head` on it and it just put out a blob of data.

Just to confirm I ran `file log.txt` to see if it recognizes anything but it said it's just a super line long of text.

`logs.txt: ASCII text, with very long lines (65536), with no line terminators`

Next I tried running `base64 -d log.txt` which outputted gibberish.

![Gibberish](images/gibberish.png)

Because of this I redirected it to another file `decoded` and ran `file decoded` which recognised the file as a png.

`decoded: PNG image data, 896 x 1152, 8-bit/color RGB, non-interlaced`

I tried running `exiftool` on the file but no good results came up so I renamed the file to `decoded.png` and opened it

![Decoded](images/decoded.png)

You might notice the text at the bottom of the image which looks like hex.

I used [this](https://www.extracttextfromimage.com/) Image to text extractor which managed to get the results I was after.

Then I ran the hex through a [hex to ascii converter](https://www.rapidtables.com/convert/number/hex-to-ascii.html) to get the flag!!!

![Flag](images/flag.png)

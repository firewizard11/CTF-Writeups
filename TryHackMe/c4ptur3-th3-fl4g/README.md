# c4ptur3-th3-fl4g

## Description

A beginner level CTF challenge

## Writeup

### Translation & Shifting

1. `c4n y0u c4p7u23 7h3 f149?`

This one is clearly just using numbers that look like the letters. So the answer is: `can you capture the flag`

2. `01101100 01100101 01110100 01110011 00100000 01110100 01110010 01111001 00100000 01110011 01101111 01101101 01100101 00100000 01100010 01101001 01101110 01100001 01110010 01111001 00100000 01101111 01110101 01110100 00100001`

For this I used the following binary decoder: <https://cryptii.com/pipes/binary-decoder>

When decoded the binary gives: `lets try some binary out!`

3. `MJQXGZJTGIQGS4ZAON2XAZLSEBRW63LNN5XCA2LOEBBVIRRHOM======`

This text is base32 since it's all capitals where and shorter than the next question which means the next one is probs **base64** as well

Using [this](https://emn178.github.io/online-tools/base32_decode.html) online decoder gave me the following text: `base32 is super common in CTF's`

4. RWFjaCBCYXNlNjQgZGlnaXQgcmVwcmVzZW50cyBleGFjdGx5IDYgYml0cyBvZiBkYXRhLg==

Continuing from the previous question I guessed this was base64 since it uses `=` padding and is longer than question 3. So using [this](https://www.base64decode.org/) decoder I got: `Each Base64 digit represents exactly 6 bits of data.` 
5. `68 65 78 61 64 65 63 69 6d 61 6c 20 6f 72 20 62 61 73 65 31 36 3f`

This just looks like hexadecimal so using [this](https://cryptii.com/pipes/hex-decoder) converter I got: `hexadecimal or base16?`

6. `Ebgngr zr 13 cynprf!`

Since this text is using a normal alphabet and the words seem word shaped we can assume it's a substitution cipher. With the number 13 in the text I'm guessing it's ROT13. Using <https://rot13.com> I got the text: `Rotate me 13 places!`. **The reason there is no decoder or encoder on this page is because applying ROT13 twice gives the original text.**

7. `*@F DA:? >6 C:89E C@F?5 323J C:89E C@F?5 Wcf E:>6DX`

This one took a while because it had a bunch of random characters but I found a pretty cool tool on this site <https://www.cachesleuth.com/multidecoder/> which just decodes the text with a bunch of different options and the most likely candidate was ROT47. The reason this includes characters like `@`,`*` and `>` because instead of shifting in the latin alphabet, this cipher shifts using the whole ascii table.

The text I got was: `You spin me right round baby right round (47 times)`

8. This one has multiple lines

```text
- . .-.. . -.-. --- -- -- ..- -. .. -.-. .- - .. --- -.
. -. -.-. --- -.. .. -. --.
```

Obviously this is morse code so I used the site <https://morsecode.world/international/translator.html>. I got the text: `TELECOMMUNICATION ENCODING`. Using this tool you can seperate words using `/` instead of putting it on another line.

9. `85 110 112 97 99 107 32 116 104 105 115 32 66 67 68`

For this one I was super confused not because it was hard but the answer made no sense to me. For this I went back tot the multi decoder which revealed the text `Unpack this BCD`

10. Ok this one is super long so I won't include it here but u might notice that it's padded using `=`. Due to this I went back to <https://www.base64decode.org/> and ran it through which interestinly gave me the following morse code.

```morse code
----- .---- .---- ----- ----- .---- .---- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- ----- .---- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- -----
----- .---- .---- ----- ----- ----- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- .---- .---- ----- .---- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- .---- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- .---- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- ----- .---- .---- .---- .---- .----
----- .---- .---- ----- ----- ----- ----- -----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
----- ----- .---- ----- ----- ----- ----- -----
----- .---- .---- ----- ----- ----- .---- .----
----- .---- .---- ----- ----- .---- ----- .----
```

Next I entered the most code in this site <https://dnschecker.org/morse-code-translator.php> which gave me some binary

```binary
011001100110010100100000011000000101111101100000001000000110000001100000011001010010000001100010011010000010000001100000011000000110010000100000011000100110000100100000011000000101111101101000001000000110100001100110001000000110000001011111011001100010000001100000010111110110000000100000011000100110000100100000011000000110000001100101001000000110000001011111011000110010000001100000010111110110010000100000011000000110000001100100001000000110001001100001001000000110100001100110001000000110001001100001001000000110100001100111001000000110000001011111011001000010000001100000011000000110010100100000011000100110000100100000011000000110000001100101001000000110000001100000011000110010000001100000010111110110010000100000011010000110100000100000011000000101111101100110001000000110000001011111011001000010000001100000010111110110000000100000011000000110000001100011001000000110001101100101001000000110001101100101001000000110001101100101
```

Putting this in a binary decoder gave me some random text that I didn't immediately get so I put it through the multi decoder and it was actually ROT47 which gave me some decimal text. I say ROT47 because it was the most legible.

```decimal
76 101 116 39 115 32 109 97 107 101 32 116 104 105 115 32 97 32 98 105 116 32 116 114 105 99 107 105 101 114 46 46 46
```

Finally using [this](https://www.prepostseo.com/tool/decimal-to-ascii) site gave me: `Let's make this a bit trickier...`

**NOTE:** I know what CyberChef is I just don't want to use it cos it's too easy.

### Spectrogram

For this challenge I just looked up `Spectrogram Decoder` and found <https://academo.org/demos/spectrum-analyzer/> and when I uploaded the file and played it gave me the text: `Super Secret Message`. It was pretty cool so I would try it out myself.

### Steganography

For this challenge I download the file `stegosteg_1559008553457.jpg` and pretty much went straight for `steghide`. Using `steghide extract -sf stegosteg_1559008553457.jpg` and no passphrase I got the text file `steganopayload2248.txt` which had the text: `SpaghettiSteg` inside.

### Security through obscurity

**Download and get 'inside' the file. What is the first filename & extension?**

Because of the phrasing of the question I thought this would be a challenge where files are inside other files so I went for `binwalk` which gave us

```text
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
30            0x1E            TIFF image data, big-endian, offset of first image directory: 8
74407         0x122A7         RAR archive data, version 5.x
74478         0x122EE         PNG image, 147 x 37, 8-bit/color RGBA, non-interlaced
74629         0x12385         Zlib compressed data, default compression
```



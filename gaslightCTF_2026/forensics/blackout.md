# blackout

## Room Info

- Points: 474
- Author: riyc
- Attachments: `recovered_file`

## Writeup

### Initial Analysis

After downloading the file I ran `file` which showed its a PDF File and `pdfinfo` which had the field `Tagged: yes` which I looked up and showed it means accessibility tags have been used in the file (which can have hidden data).

### Fake Redaction

Next I did a visual inspection and it showed that the file has "redacted" text but instead of actually redacting it looks like black boxes overlayed so you can highlight the text and see the content.

### Finding the Flag

Now I didnt really know how to dump the text because I wanted to grep for the flag so I found the option `pdfinfo -struct-text` which will dump the content of tagged files including the tags as text.

`pdfinfo -struct-text recovered_file | grep gaslightCTF` which revealed the flag `gaslightCTF{[REDACTED]}`

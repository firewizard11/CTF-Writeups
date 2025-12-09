# PW Crack 2

## Description

Can you crack the password to get the flag?

## Approach

This time we are given the following files:

![Files](images/file.png)

This time in the source code the password is obfuscated using the `char()` and concatenation.

![PW Check Function](images/func.png)

We can actually just get plain text string by copying the `char()` functions and wrapping them in a `print()` function inside the python interpreter

![PW](images/pw.png)

Now we can enter the password and get the flag

![Flag](images/flag.png)

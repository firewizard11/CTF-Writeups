# 2Warm

## Description

Can you convert the number 42 (base 10) to binary (base 2)?

## Approach

We can convert base 10 to base 2 by first finding the highest power of 2 before 42 which is 32.

42 - 32 = 10 and the highest power of 2 under 10 is 8.

Following the process we get:

- 10 - 8 = 2
- 2 - 2 = 0

Using these numbers we get the values 2^5 + 2^3 + 2^1 = 42, Which corresponds to the binary 101010

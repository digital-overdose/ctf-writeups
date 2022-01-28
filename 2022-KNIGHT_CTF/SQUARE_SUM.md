# Square Sum

- Date: `2022-01-28`
- Author: `AtomicNicos`
- Category: `Programming`
- Points: `50`

## Challenge text

Have you ever heard the term "The sum of two squares"?

It's like the following :

```txt
4 = 0^2 + 2^2
8 = 2^2 + 2^2
16 = 0^2 + 4^2
----------------------------
5002 = 39^2 + 59^2 => 49^2 + 51^2 => 51^2 + 49^2 => 59^2 + 39^2
```

And so on. In the example of 16, if we add the square of 0 & 4 we get 16. So here we are getting two values 0 & 4. So that's the answer.

So write a program & find out the two values of 25000. Conditions are the following :

- Remove the duplicates
- Pick the third one

Flag Format: `KCTF{0,1}`

## Description

We can produce an algorithm that loops between both bounds (or more accurately the square root of both bounds).

## Resolution

This can quite easily be written in Python:

```py
from math import sqrt

for i in range(round(sqrt(25000))):
    for j in range(round(sqrt(25000)), -1, -1):
        if i ** 2 + j ** 2 == 25000:
            print(f"{i} ** 2 + {j} ** 2")
```

This produces:

```txt
6 ** 2 + 158 ** 2
50 ** 2 + 150 ** 2
90 ** 2 + 130 ** 2
130 ** 2 + 90 ** 2
150 ** 2 + 50 ** 2
```

We can remove the duplicates:

```txt
6 ** 2 + 158 ** 2
50 ** 2 + 150 ** 2
90 ** 2 + 130 ** 2
```

The third result is `90, 130` so the flag is `KCTF{90,130}`.

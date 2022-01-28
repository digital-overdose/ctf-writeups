# Reverse the Answer

- Date: `2022-01-28`
- Author: `AtomicNicos`
- Category: `Programming`
- Points: `50`

## Challenge text

Let x = 1

Let calculation = (x*(x+1)) + (2 *(x + 1))

Let reversed_calc = reversed number of calculation [for example if calculation = 123, reversed_calc will be 321]

If reversed_calc can be divided by 4 without reminder then answer = answer + reversed_calc

Repeat all the calculations until you have x = 543

The final answer will be the flag when x = 543

Flag Format : `KCTF{answer_here}`
Example Flag : `KCTF{123}`

## Description

Reverse an algorithm.

## Resolution

We perform the loop for x going from 1 to 543.

To facilitate the calculation, we write the following program, in Python:

```py
x = 1
answer = 0

while x <= 543:
    calculation = (x + 2) * (x + 1)
    rev = int(str(calculation)[::-1])
    if rev % 4 == 0:
        answer += rev
    x += 1

print(answer)
```

This produces `12252696`, so the flag is `KCTF{12252696}`.
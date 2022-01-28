# Alphabet Knock Code

- Date: `2022-01-28`
- Author: `AtomicNicos`
- Category: `Cryptography`
- Points: `100`

## Challenge text

My friend send me this file and told me that C=K ,Y=Z total number is 24 . But I can not understand this. Can you help me?

[Download link](https://kctf2022.nstechvalley.com/knight-ctf-2022-challenges/Cryptography/AlphabetknockCode/knock.txt)

Flag Format: `KCTF{FLAGHERE}`

## Description

This is using an implementation of the [Tap Code](https://en.wikipedia.org/wiki/Tap_code) but instead of a 5x5 grid:

|   | 1 | 2 |  3  | 4 | 5 |
|:-:|:-:|:-:|:---:|:-:|:-:|
| 1 | A | B | C/K | D | E |
| 2 | F | G |  H  | I | J |
| 3 | L | M |  N  | O | P |
| 4 | Q | R |  S  | T | U |
| 5 | V | W |  X  | Y | Z |

...we use a 24=4x6 grid:

|   | 1 | 2 |  3  | 4 | 5 | 6   |
|:-:|:-:|:-:|:---:|:-:|:-:|:---:|
| 1 | A | B | C/K | D | E | F   |
| 2 | G | H |  I  | J | L | M   |
| 3 | N | O |  P  | Q | R | S   |
| 4 | T | U |  V  | W | X | Y/Z |

The message is: `... ......  . .....  . ...  ... .....  . .....  .... ..  . ...  ... .  .. ...  .. .  .. ..  .... ..`

## Resolution

We first notice the double-spacing, so we can split the message into a few charaters:

```txt
... ...... -> 3,6
. .....    -> 1,5
. ...      -> 1,3
... .....  -> 3,5
. .....    -> 1,5
.... ..    -> 4,2
. ...      -> 1,3
... .      -> 3,1
.. ...     -> 2,3
.. .       -> 2,1
.. ..      -> 2,2
.... ..    -> 4,2
```

The code should be:

```txt
... ...... -> 3,6 -> s
. .....    -> 1,5 -> e
. ...      -> 1,3 -> c/k
... .....  -> 3,5 -> r
. .....    -> 1,5 -> e
.... ..    -> 4,2 -> u
. ...      -> 1,3 -> c/k
... .      -> 3,1 -> n
.. ...     -> 2,3 -> i
.. .       -> 2,1 -> g
.. ..      -> 2,2 -> h
.... ..    -> 4,2 -> u
```

This spells out `se(c|k)reu(c|k)nighu`. This... doesn't make much sense, but we can already guess the result as being `secretknight`. There must have been an issue with the encryption script.

The flag is `KCTF{secretknight}`

# DROID FLAG

- Date: `2022-01-25`
- Author: `AtomicNicos`
- Category: `Cryptography`
- Points: `150`

## Challenge text

My friend Ridwan is interested into ciphers lately. He sent me the encrypted flag. Can you help me decrypt?

[Download Link](https://kctf2022.nstechvalley.com/knight-ctf-2022-challenges/Cryptography/Feistival/)

Flag Format: `KCTF{some_text_here}`

## Description

Download the code and the cipher, reverse the code, read the plaintext.

## Resolution

Download the cipher and open it:

```txt
H@WExefjpwfo5(## 
```

Download the code and open it:

```py
m, n = 21, 22
def f(word, key):
    out = ""
    for i in range(len(word)):
        out += chr(ord(word[i]) ^ key)
    return out

flag = open("flag.txt", "r").read()

L, R = flag[0:len(flag)//2], flag[len(flag)//2:]
x = "".join(chr(ord(f(R, m)[i]) ^ ord(L[i])) for i in range(len(L)))
y = f(R, 0)

L, R = y, x
x = "".join(chr(ord(f(R, n)[i]) ^ ord(L[i])) for i in range(len(L)))
y = f(R, 0)

ciphertext = x + y
ct = open("cipher.txt", "w")
ct.write(ciphertext)
ct.close()
```

This code is a bit ugly (imo) because it is very non-functional: you provide an array to be filled as a parameter, which feels wrong.

The f function just XOR's the ASCII values of the provided word with 0.

The flag is read then split into two parts.

The left's ASCII values are XOR'ed with the right's values XOR'ed with the constant `m` (23).

Left and right are inverted.

The new right's (old left's) ASCII values are XOR'ed with the left's (old-right's) values XOR'ed with the constant `n` (22).

The right element is then called on the right portion.

Both sides are apeneded to one another, and saved to a file.

<br/>
To reverse this, we must perform the steps backwards:

```py
def f(word, key):
    out = ""
    for i in range(len(word)):
        out += chr(ord(word[i]) ^ key)
    return out

m, n = 21, 22

ct = open("cipher.txt", "r")
ciphertext = ct.read()
ct.close()

L, R = ciphertext[0:len(ciphertext)//2], ciphertext[len(ciphertext)//2:]
y = f(R, 0)
x = "".join(chr(ord(f(R, n)[i]) ^ ord(L[i])) for i in range(len(L)))
L, R = y, x

y = f(R, 0)
x = "".join(chr(ord(f(R, m)[i]) ^ ord(L[i])) for i in range(len(L)))

flag = x + y

f = open("plain.txt", "w")
f.write(flag)
f.close()
```

This produces the file `plain.txt` which contains the following: `KCTF{feistel_cipher_ftw}`
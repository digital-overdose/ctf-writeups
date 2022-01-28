# RSA-One

- Date: `2022-01-28`
- Author: `AtomicNicos`
- Category: `Cryptography`
- Points: `100`

## Challenge text

Our security agency has got hold of a ciphertext and a key. Well..the key got corrupted and the lost character is represented by a x. Can you decipher the message for us?

[Download link](https://kctf2022.nstechvalley.com/knight-ctf-2022-challenges/Cryptography/RSA-One/)

Flag Format: `KCTF{S0m3_T3xt_H3re}`

## Description

The downloaded cert file has an extra symbol in it (part omitted for brevity):

```txt
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAyiytHt1AKzYLwZPm1dd9uT7LgsqVj0eSLpheNd0H4xyiZCYG
ZtRYnNtGNnq7A/ubyFalExm61QNewfy71h6xhM/❌IEIoNT0VfMOIzcq0Jmoh+v6k
6/x/3GRkk/vLVolsLbkOKd4aorPMwEsZX4vMd+Sga5Mz0tx5xLFZsbl0r1vvtBl7
...
xqG9YAHVmm4iJzcHeMdzLwmzR6D/x6+k2cFWwox6PxvA7ikJQEYr
-----END RSA PRIVATE KEY-----
```

We attempt to generate every other cert out there to test it.

## Resolution

Step one is generating each cert, for which we use Python (assumes a directory `./certs` exists, and that private.pem is in the cwd):

```py
from codecs import open as copen
import string

f = copen('private.pem', mode='r', encoding='utf-8')
d = f.readlines()
f.close()

print(d[2][39])

j = 0
for i in list(string.ascii_letters) + list(string.digits) + ['+']:
    print(i)
    d[2] = list(d[2])
    d[2][39] = i
    d[2] = "".join(d[2])
    f = copen(f'certs/private-{i}.pem', mode='w', encoding='utf-8')
    f.writelines(d)
    f.close()
```

We can then test each cert using `openssl rsautl` by finding and applying them to the flag (cwd = `./certs` , assumes the upper directory has a `./public/` directory):

```sh
find -type f -wholename "./private-*.pem" -exec sh -c 'echo $0; SUBSTR=$(echo $0 | cut -d'/' -f 2); openssl rsautl -decrypt -inkey $0 -in ../flag.enc -out "../public/decoded-${SUBSTR}" 2>/dev/null' {} \;
```

We can then use `find /tmp -size  0 -print -delete` to delete all empty files leaving `decoded-private-a.pem` which contains the flag: `KCTF{M4Y_TH3_8RUT3F0rc3_B3_W1TH_Y0U}`

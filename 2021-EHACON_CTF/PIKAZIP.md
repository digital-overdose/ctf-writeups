# CHALLENGE NAME

- Date: `2021-11-10`
- Author: `AtomicNicos`

## Description

Nested compressed files, except with varying formats (`rar` -> `tar.gz` -> `tar` -> `zip` -> `rar` -> `...`).

## Resolution

TODO: Finish

```py
from os import walk, system, remove

while True:
    filenames = next(walk("."), (None, None, []))[2]  # [] if no file
    filenames = list(filter(lambda x: not x.endswith(".py"), filenames))
    fname = filenames[0]
    print(fname)
    if fname.endswith(".rar"):
        system(f"unrar x {fname}")
        remove("./" + fname)
    elif fname.endswith(".gz"):
        system(f"gunzip {fname}")
    elif fname.endswith(".tar"):
        system(f"tar -xvf {fname}")
        remove("./" + fname)
    elif fname.endswith(".zip"):
        system(f"unzip {fname}")
        remove("./" + fname)
    else:
        break
```

```txt
pi pi pi pi pi pi pi pi pi pi pika pipi pi pipi pi pi pi pipi pi pi pi pi pi pi pi pipi pi pi pi pi pi pi pi pi pi pi pichu pichu pichu pichu ka chu pipi pipi pipi ka pikachu pi pi pi pikachu ka ka ka ka ka ka ka pikachu pi pi pikachu pi pi pi pi pi pi pi pi pi pi pi pi pikachu ka pikachu pipi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pikachu ka ka ka ka ka ka ka ka ka ka ka ka ka pikachu pichu pichu pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pikachu pi pi pi pi pi pi pi pikachu pipi pipi ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka pikachu pichu pichu pikachu ka ka ka ka ka ka pikachu pipi pipi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pikachu pichu pichu pi pi pikachu pipi pipi ka ka ka ka ka ka ka ka ka ka ka ka ka ka pikachu ka ka ka ka ka pikachu pichu pichu ka ka ka pikachu pipi pipi pi pi pi pi pi pi pi pikachu ka ka ka ka ka ka ka pikachu pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pikachu ka ka ka ka ka ka ka pikachu pi pi pi pi pi pi pi pi pi pi pi pi pikachu pichu pichu pi pikachu pipi pipi ka ka ka ka ka ka ka ka ka ka pikachu pikachu pichu pichu pikachu pipi pipi ka ka pikachu pichu pichu pi pi pi pi pi pikachu pipi pipi ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka pikachu pi pi pi pi pi pi pi pi pi pikachu pi pi pi pi pi pi pi pi pi pi pi pi pi pikachu ka ka ka ka ka ka ka ka ka ka ka ka ka pikachu pichu pichu ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka ka pikachu pikachu pikachu pipi pipi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pi pikachu
```

## Takeaways (optional)

What you consider made this challenge interesting and unique.

## Rating (optional)

A difficulty rating (arbitrarily `x/5`) you give for this challenge.

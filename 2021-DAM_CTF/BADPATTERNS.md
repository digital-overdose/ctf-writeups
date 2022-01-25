# Bad Patterns

- Date: `2021-11-12`
- Author: `JustAnotherPenTester`

## Description

A hacker was too lazy to do proper encryption. However, they left us some examples of how their encryption "algo" was supposed to work.

original text :
```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```

encoded:
```
Lpthq jrvym!frpos"vmt!cpit-"fsntgfxeuwu$aeksmsdkqk fnlx,!uhh eq#iivupsd!vhqppt#mndkgmdvpw$uu"oebpth$eu"gslpth$mbiqe bnluub0#Yt!gqmm!cg$mjplq wgqman.#uuju#rotvuyd!g{irdkwetjqq$umndqcp"oebptlw okvm vv#eljsxmp!g{$eb"fsmnqgs dqqwerwdx.!Fxms!cxxe!kuyrf"gslpt#mn!thtrfjhrdftlx jp#zomwsxaug#zemkw$etuh$cjnoym!frposg#iu!hxkibv#rumnd$pbtletvt1$Eyehttfwu$sjpw$odedicbv#guqkgetbv#roo"svojfhrt-"vynu"lr dwota!sxm phimcjc#hetguynu"pslmkw$aokp$ie"hwt!ndfoswp2
```

Find the pattern!

Maybe you should try the same pattern on this string:

"bagelarenotwholewheatsometimes"


## Resolution

Comparing the first words from original text and encoded we can decipher the pattern.
| Original | Encoded | Position | Increment |
| -------- | ------- | -------- | -------- |
| L | L | 0 | 0 |
| o | p | 1 | 1 |
| r | t | 2 | 2 |
| e | h | 3 | 3 |
| m | q | 4 | 4 |
| \<space\> | \<space\> | 5 | 0 |
| i | j | 6 | 1 |

Each character's ascii value is incremented by its position and the increment gets reset at every 5th position.
Positions are counted from 0 and not 1.

Thats why L remains L, o becomes p, r becomes t and so on.
And when we reach the \<space\> character, it remains \<space\> as its position is 5.

Using a simple script to implement the pattern, we can get the flag

```
plaintext = "bagelarenotwholewheatsometimes"
encodedtext= ""
count = 0

for i in plaintext:
  encodedtext += chr(ord(i) + (count%5))
  count += 1

print(encodedtext)
```

The output wrapped with "dam{}" gives the flag: `dam{bbihpasgqstxjrpexjhettqpitjohw}`

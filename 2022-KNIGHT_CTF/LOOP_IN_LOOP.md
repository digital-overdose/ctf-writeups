# Loop in a Loop

- Date: `2022-01-25`
- Author: `AtomicNicos`
- Category: `Programming`
- Points: `100`

## Challenge text

We use the file to verify our flags. Can you retrieve it?

[Download Link](https://kctf2022.nstechvalley.com/knight-ctf-2022-challenges/Programming/Loop%20In%20A%20Loop/flag.cpp)

Flag Format: `KCTF{Fl4g_H3re}`

## Description

Read the code and reverse it.

## Resolution

Download the C++ code and open it:

```cpp
#include <iostream>
using namespace std;

int main() {
    string flag;
    cout << "Enter the flag: ";
    cin >> flag;

    for (int i=0; i < flag.length(); i++) {
        for (int j=i; j < flag.length() - 1; j++) {
            char x = flag[j];
            flag[j] = flag[j+1];
            flag[j+1] = x;
        }
    }

    if (flag == "CFb5cp0rm1gK{1r4nT_m4}6")
        cout << "Congrats. That's the flag!" << endl;
    else
        cout << "Wrong flag. Bye" << endl;

    return 0;
}
```

I rarely do CPP and never when I could use something else, so the solution will be in Python.

But first, analysis:

- The code takes a flag as input:
- It then loops on all indices, and then initiates a second loop on **all remaining** indices.
- The code inverts the characters at positions `j` and `j+1`.

To reverse this we do the exact same loop with reversed parameters (`i: length -> 0, j: length -> i`), and then print the original flag:

```py
flag = list("CFb5cp0rm1gK{1r4nT_m4}6")

for i in range(len(flag) - 1, -1, -1):
    for j in range(len(flag) - 1, i, -1):
        flag[j], flag[j-1] = flag[j-1], flag[j]

print("".join(flag))
```

The flag is `KCTF{b451c_pr06r4mm1ng}`

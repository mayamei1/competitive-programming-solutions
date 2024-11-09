---
tags:
  - competitive-programming/judges/ieeextreme
name: Caesar Redux
date: 2023-10-28
---
#competitive-programming/trivial
## _Solution:_
Simple shift/Caesar cypher. Check for the word "the" to determine encoding or decoding.

```cpp
n = int(input())

for i in range(n):
    a = int(input())
    s = input()

    plain = "the" in s.split()
    ans = ""
    for i in s:
        if i != ' ':
            if plain: val = chr(((ord(i) - ord('a') - a) % 26) + ord('a'))
            else: val = chr(((ord(i) - ord('a') + a) % 26) + ord('a'))
        else: val = ' '
        ans += val
    print(ans)
```
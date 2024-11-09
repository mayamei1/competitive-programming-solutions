---
tags:
  - competitive-programming/judges/kattis
name: Hay Points
date: 2019-03
---
#competitive-programming/trivial 
## _Solution:_
Simply use a map and count the value of each line.

https://open.kattis.com/problems/haypoints
```python
m, n = map(int, input().split())

val = {}
for i in range(m):
    w, v = input().split()
    val[w] = int(v)

for i in range(n):
    s = input()
    ans = 0
    while s != ".":
        for w in s.split():
            if w in val:
                ans += val[w]
        s = input()
    print(ans)

```
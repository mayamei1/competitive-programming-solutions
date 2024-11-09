---
tags:
  - competitive-programming/judges/hackerrank
name: Belly Flop Bonanza
date: 2024-10-26
---
#competitive-programming/math #competitive-programming/sorting 
## _Solution:_
For each athlete, calculate the distance from origin, and add the radius. Then, sort the athletes by this value.

https://www.hackerrank.com/contests/lpc-2024/challenges/belly-flop-bonanza
```python
n = int(input())

a = []
for i in range(n):
    name, coords, r = input().split("; ")
    name = name.strip()
    x, y = map(float, coords[1:-1].split(", "))
    r = float(r)
    a.append([name, (x * x + y * y) ** 0.5 + r / 2])

a = list(reversed(sorted(a, key=lambda x: x[1])))

for i in range(3):
    print(a[i][0])
```
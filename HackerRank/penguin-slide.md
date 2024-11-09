---
tags:
  - competitive-programming/judges/hackerrank
name: Penguin Slide
date: 2024-10-26
---
#competitive-programming/sorting 
## _Solution:_
Simply sort by the corresponding number.

https://www.hackerrank.com/contests/lpc-2024/challenges/penguin-slide
```cpp
n = int(input())

a = []

for i in range(n):
    s = input().split()
    name = ' '.join(s[0:-2])
    num = int(s[-1])
    a.append((num, name))

a = sorted(a)
print("First:", a[0][1])
print("Second:", a[1][1])
print("Third:", a[2][1])
```
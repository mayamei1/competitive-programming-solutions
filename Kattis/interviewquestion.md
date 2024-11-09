---
tags:
  - competitive-programming/judges/kattis
name: Interview Question
date: 2024-11-03
---
#competitive-programming/math/gcd 
## _Solution:_
Since Fizz and Buzz are guaranteed to exist, we can simply find the GCD of all numbers with Fizz, and the same with Buzz. If no elements exist with Fizz, then we can set it to $r+1$. Same with Buzz and $r+2$.

https://open.kattis.com/problems/interviewquestion
```python
from math import *

l, r = map(int, input().split())

a = input().split()

b = zip(range(l, r + 1), a)

fizz, buzz = -1, -1

for i, x in b:
    if x == "Fizz":
        if fizz == -1:
            fizz = i
        else:
            fizz = gcd(fizz, i)
    elif x == "Buzz":
        if buzz == -1:
            buzz = i
        else:
            buzz = gcd(buzz, i)
    elif x == "FizzBuzz":
        if fizz == -1:
            fizz = i
        else:
            fizz = gcd(fizz, i)
        if buzz == -1:
            buzz = i
        else:
            buzz = gcd(buzz, i)

if fizz == -1: fizz = r + 1
if buzz == -1: buzz = r + 2

print(fizz, buzz)
```
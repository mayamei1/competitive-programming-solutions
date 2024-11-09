---
tags:
  - competitive-programming/judges/kattis
name: Persistent Numbers
date: 2019-03-20
---
#competitive-programming/greedy #competitive-programming/math 
## _Solution:_
Greedily try to divide by the largest digit ($9$) as many times as possible first. Then, try to divide by $8$ as many times as possible. Keep doing this down to $2$. Then, the answer is the concatenation of every time you divided by $2$, then with $3$, so on until $9$. The edge case of $a<10$, the answer is $a+10$. This problem requires integers larger than 64-bits.

https://open.kattis.com/problems/persistent
```python
while True:
    a = int(input())

    if a == -1: break
    
    if a < 10:
        print(10 + a)
        continue

    count = [0] * 10

    for d in reversed(range(2, 10)):
        while a % d == 0:
            a //= d
            count[d] += 1
    
    if a != 1:
        print("There is no such number.")
        continue

    for d in range(2, 10):
        for dd in range(count[d]):
            print(d, end='')
    print()
```
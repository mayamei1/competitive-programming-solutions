---
tags:
  - competitive-programming/judges/kattis
name: Catalan Numbers
date: 2024-01-12
---
#competitive-programming/math/combinatorics
## _Solution:_
Calculate the $n$th Catalan number with the following equation $c_n=\frac{(2n)!}{(n+1)!n!}$. The numbers are much larger than 64-bit integers. Keep track of factorials up to $10000$.

https://open.kattis.com/problems/catalan
```python3
q = int(input())

fact = [1]
prod = 1
for i in range(1, 10001):
    prod *= i
    fact.append(prod)

for i in range(q):
    x = int(input())
    print(fact[2*x]//fact[x+1]//fact[x])
```
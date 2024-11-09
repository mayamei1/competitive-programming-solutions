---
tags:
  - competitive-programming/judges/kattis
name: Best Compression
date: 2021-10-11
---
#competitive-programming/math/combinatorics
## _Solution:_
Check if $n\leq 2^{b+1}-1$.

https://open.kattis.com/problems/bestcompression
```python
n,b = [int(x) for x in input().split()]

if (n <= 2 ** (b + 1) - 1):
    print('yes')
else:
    print('no')
```
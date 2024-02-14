---
type:
  - competitive-programming
  - kattis
tags:
  - math/combinatorics
name: Best Compression
---
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
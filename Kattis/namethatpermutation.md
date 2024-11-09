---
tags:
  - competitive-programming/judges/kattis
name: Name That Permutation
date: 2024-04-01
---
#competitive-programming/math/combinatorics 
#competitive-programming/permutation 
## _Solution:_
Given a set of ordered digits $d$ of length $n$, finding the $k$-th permutation, you can find out the first digit of that permutation by getting the $\lfloor \frac{k}{(n-1)!}\rfloor$th digit ($0$-indexed). This digit needs to be removed from the ordered set, and it is now a subset of the problem with the new $d$ with a new length $n$, and $k_{new}=k_{old}\mod{(n_{old}-1)!}$. Big integers must be used.

https://open.kattis.com/problems/namethatpermutation
```python
import math

f = math.factorial

ans = []
def solve(d, k):
    n = len(d)
    if n == 0:
        return
    cd = d[k // f(n - 1)]
    ans.append(cd)
    dn = [dd for dd in d if dd != cd]
    solve(dn, k % f(n - 1))

while True:
    try:
        n, k = map(int, input().split())
    except:
        break
    ans = []
    solve(list(range(1, n + 1)), k)
    for a in ans:
        print(a, end=' ')
    print()
```
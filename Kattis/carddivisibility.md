---
tags:
  - competitive-programming/judges/kattis
name: Card Divisibility
date: 2023-04-05
---
#competitive-programming/math/modular-arithmetic
## _Solution:_
Divisibility by nine can be found by checking if the sum of it's digits is divisible by nine. If we perform the sums over subgroups, then sum over the sums, the same is still true. So we can say that those groups are numbers between $l$ and $r$. Thus, we simply need to check if the sum of numbers between $l$ and $r$ is divisible by nine.

https://open.kattis.com/problems/carddivisibility
```python
l,r = [int(x) for x in input().split()]
sum=((r*(r+1)//2)%9-(l*(l+1)//2)%9+l%9)%9
print(sum)
```

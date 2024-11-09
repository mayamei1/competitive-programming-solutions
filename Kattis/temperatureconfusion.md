---
tags:
  - competitive-programming/judges/kattis
name: Temperature Confusion
date: 2024-04-08
---
#competitive-programming/math/gcd 
## _Solution:_
Manually do fraction operations.

https://open.kattis.com/problems/temperatureconfusion
```python
import math

gcd = math.gcd

a, b = map(int, input().split('/'))

a, b = a - 32 * b, b
g = gcd(a,b)
a, b = a // g, b // g
a, b = a * 5, b * 9
g = gcd(a,b)
a, b = a // g, b // g

print(f"{a}/{b}")
```
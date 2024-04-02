---
tags:
  - competitive-programming/catalog/kattis
name: Smallest Multiple
---
#competitive-programming/math/gcd 
## _Solution:_
Simple LCM of every number. Big integers must be used.

https://open.kattis.com/problems/smallestmultiple
```python
import math

def lcm(a, b):
    return abs(a*b) // math.gcd(a, b)

while True:
    try:
        a = map(int, input().split())
    except:
        break

    ans = 1
    for ai in a:
        ans = lcm(ans, ai)
    
    print(ans)
```
---
tags:
  - competitive-programming/judges/kattis
name: Pretty Good Cube Root
date: 2024-04-02
---
#competitive-programming/binary-search 
## _Solution:_
Binary search to find the integer with the smallest difference between $m^3$ and $n$. Big integers must be used.

https://open.kattis.com/problems/prettygoodcuberoot
```python
while True:
    try:
        n = int(input())
    except:
        break

    l, h = 0, n
    ans = 1
    diff = n - 1
    while l <= h:
        m = l + (h - l) // 2
        o_diff = m * m * m - n
        
        if abs(o_diff) < diff:
            ans = m
            diff = abs(o_diff)
        
        if o_diff == 0:
            break
        elif o_diff > 0:
            h = m - 1
        else:
            l = m + 1
    
    print(ans)
```
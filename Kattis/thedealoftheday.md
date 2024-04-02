---
tags:
  - competitive-programming/catalog/kattis
name: The Deal of the Day
---
#competitive-programming/complete-search #competitive-programming/math/combinatorics #competitive-programming/bitmask 
## _Solution:_
Iterate through each possible subset with a bitmask and add to the solution if there are exactly $K$ elements in the subset. The number of possible solutions with that particular subset can be found with multiplication of number of cards of each element. Big integers must be used.

https://open.kattis.com/problems/thedealoftheday
```python
import math

a = list(map(int, input().split()))
k = int(input())

ans = 0
for mask in range(1 << 10):
    ans1 = 1
    count = 0
    for i in range(10):
        ans1 *= a[i] if ((mask >> i) & 1) else 1
        count += (mask >> i) & 1
    if count == k: ans += ans1

print(ans)
```
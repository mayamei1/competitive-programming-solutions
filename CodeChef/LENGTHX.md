---
tags:
  - competitive-programming/judges/codechef
name: Pairs Sum with Length x
date: 2024-07-10
---
#competitive-programming/segment-tree #competitive-programming/coordinate-compression
## _Solution:_
An equivalent problem is, for each pair, how many subranges does it contribute to. For a particular pair $a_i$ and $a_j$ ($j<i$), the following must be true: $10^{x-1}\le a_{i}+a_{j}\le10^{x}-1$. All of the subranges that the pair contributes to are where the left bound is anywhere in the prefix up to $j$ and the right bound is anywhere in the suffix up to $i$, giving a contribution of $j\cdot(n-i+1)$. Then, to efficiently calculate total contribution of every pair, we can use a segment tree with coordinate compression. Iterating through each $a_i$, we check the segment tree for the sum of $j$ for all $a_j$ between $10^{x-1}$ and $10^{x}-1$. Multiply the sum with $n-i+1$. Then, add $i$ to the segment tree for $a_i$.

https://www.codechef.com/problems/LENGTHX
```python
import bisect

def solve():
    n, x = map(int, input().split())
    a = list(map(int, input().split()))
    b = sorted(list(set(a)))
    m = len(b)
    bit = [0] * (m + 1)

    def add(i, delta):
        i += 1
        while (i < len(bit)):
            bit[i] += delta
            i += (i & (-i))
    
    def sum(i):
        val = 0
        i += 1
        while (i > 0):
            val += bit[i]
            i -= (i & (-i))
        return val
    
    l, h = 10 ** (x - 1) - 1, 10 ** (x) - 1
    ans = 0
    for i in range(n):
        if (a[i] > h): continue
        ajh = max(0, h - a[i])
        ajl = max(0, l - a[i])
        ih = bisect.bisect(b, ajh) - 1
        il = bisect.bisect(b, ajl) - 1
        sumh = sum(ih)
        suml = sum(il)
        ans += (sumh - suml) * (n - i)
        icur = bisect.bisect_left(b, a[i])
        add(icur, i + 1)
    print(ans)

t = int(input())
for i in range(t):
    solve()
```
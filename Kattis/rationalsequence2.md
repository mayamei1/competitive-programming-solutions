---
tags:
  - competitive-programming/judges/kattis
name: A Rational Sequence 2
date: 2019-11-21
---
#competitive-programming/math #competitive-programming/graph/tree 
## _Solution:_
You can determine whether you are in the left or right child based on if $p$ is greater than $q$. Going up the binary tree, you can represent the moves as binary values to get the final answer.

https://open.kattis.com/problems/rationalsequence2
```python
def solve():
    t, pq = input().split()
    t = int(t)
    p,q = map(int, pq.split('/'))
    
    n = 0
    h = 0
    while p != q:
        if p > q:
            n += 1 << h
            p -= q
        else:
            q -= p
        h += 1
    n += 1 << h
    print(t, n)


t = int(input())
while t != 0:
    solve()
    t -= 1
```
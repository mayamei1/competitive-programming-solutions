---
tags:
  - competitive-programming/judges/hackerrank
name: Gymnastics Routine Maker
date: 2024-10-26
---
#competitive-programming/dp 
## _Solution:_
Keep track of a two state DP table: $i$ denoting the $i$-th move executed, and $j$ denoting the current move. We also create an adjacency list for which moves that can proceed the current move. Then, the DP recurrence is simple, as you keep track of the maximum score at $(i,j)$. Then, the answer is simply the maximum element across $(10,j)$, where $1\le j\le n$.

https://www.hackerrank.com/contests/lpc-2024/challenges/gymnastics-routine-maker
```python
n = int(input())

adj = [[] for x in range(n)]
ws = [0] * n

dist = [[-1] * 10 for x in range(n)]

q = [-1] * n
inv = {}
id = 0

for i in range(n):
    s = input().split()
    move = s[0]
    if move not in inv:
        inv[move] = id
        id += 1
    u = inv[move]
    ws[u] = int(s[1]) * int(s[2])
    for p in s[3:]:
        if p == "start":
            q[u] = ws[u]
            continue
        if p not in inv:
            inv[p] = id
            id += 1
        v = inv[p]
        adj[v].append(u)

for i in range(9):
    nq = [-1] * n
    for u in range(n):
        if q[u] == -1: continue
        for v in adj[u]:
            nq[v] = max(nq[v], q[u] + ws[v])
    q = nq

ans = 0
for x in q:
    ans = max(ans, x)

print('{:.3f}'.format(ans / 1000))
```
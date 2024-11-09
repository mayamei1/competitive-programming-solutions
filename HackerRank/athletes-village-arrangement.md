---
tags:
  - competitive-programming/judges/hackerrank
name: Athletes' Village Arrangement
date: 2024-10-26
---
#competitive-programming/complete-search #competitive-programming/graph 
## _Solution:_
This is a well known NP-hard problem. Simply perform backtracking in order to try every possibility. Make sure to check that for every edge you traverse, there must also be a back edge. Also, for the last element, be sure that there is also an edge to the first element.

https://www.hackerrank.com/contests/lpc-2024/challenges/athletes-village-arrangement
```python
n = int(input())

a = [""] * n
edges = [[] for x in range(n)]
for i in range(n):
    a[i] = input()
    others = input().split()
    for o in others:
        edges[i].append(o)
inv = {}
for i in range(n):
    inv[a[i]] = i

adj = [[] for x in range(n)]
for i in range(n):
    for o in edges[i]:
        adj[i].append(inv[o])

vis = [False] * n
def dfs(u, p, cnt):
    flag = (p == -1)
    flag2 = False
    for v in adj[u]:
        if v == p: flag = True
        if v == 0: flag2 = True
    if flag == False: return False

    if (cnt == n):
        return flag2

    vis[u] = True
    for v in adj[u]:
        if vis[v]: continue
        if dfs(v, u, cnt + 1): return True
    vis[u] = False
    
    return False

if (dfs(0, -1, 1)): print("true")
else: print("false")

```
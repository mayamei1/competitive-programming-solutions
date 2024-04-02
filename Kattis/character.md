---
tags:
  - competitive-programming/catalog/kattis
name: Character Development
---
#competitive-programming/math/combinatorics
## _Solution:_
$O(n)$ solution: Count every $_nC_i$ for $i$ between $2$ and $n$.

$O(1)$ solution: Count every possible set, but remove sets with size 1.

https://open.kattis.com/problems/character
```python
n = int(input())

fact = []
fact.append(1)

for i in range(1, n + 1):
  fact.append(fact[i - 1] * i)

comb_sum = 0
for r in range(2, n + 1):
  comb_sum += fact[n] // (fact[r] * fact[n - r])

print(comb_sum)
```
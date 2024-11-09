---
tags:
  - competitive-programming/judges/kattis
name: Babelfish
date: 2019-10-13
---
#competitive-programming/string #competitive-programming/trivial 
## _Solution:_
Simply keep a mapping of translations.

https://open.kattis.com/problems/babelfish
```python
map = {}
while True:
    s = input()
    if s == "":
        break
    u, v = s.split()
    map[v] = u

while True:
    try:
        s = input()
        if s in map:
            print(map[s])
        else:
            print("eh")
    except:
        break
```
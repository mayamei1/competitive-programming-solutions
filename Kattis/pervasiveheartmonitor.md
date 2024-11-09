---
tags:
  - competitive-programming/judges/kattis
name: Pervasive Heart Monitor
date: 2019-03-20
---
#competitive-programming/trivial 
## _Solution:_
This is a parsing problem :)


```python
while True:
    try:
        s = input().split()
    except:
        break

    name = ""
    count = 0
    sum = 0
    for w in s:
        try:
            sum += float(w)
            count += 1
        except:
            name += w + " "
    print(f"{sum / count} {name}")
```
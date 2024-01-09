---
type:
  - competitive-programming
  - kattis
tags:
  - math/modular-arithmetic
---
#kattis #kattis-carddivisibility

## _Solution:_
Divisibility of 9 can be found by adding the sum of digits. Same can be done with modulo 9. [[Modular Arithmetic#Addition, subtraction, multiplication|Modular arithmetic]] says that we can split the digits into sections as well . Ex: $1234\%m=((1\%9)+(2\%9)+(3\%9)+(4\%9))\%9$. But it can also be recombined by summing, ex: $(1+2+3+4)\%9$. Which means, you can find the answer by summing all numbers between `L` and `R`.

Sum between $1$ and $n$ is $\frac{n*(n+1)}{2}$. So sum between $l$ and $r$ (inclusive) is `r*(r+1)/2 - l*(l+1)/2 + l`. In order to get the answer, you can throw a `% 9` at the end. Now, in order to keep the value small, and therefore calculation time small, use modular arithmetic (`% 9`'s everywhere ‼).

https://open.kattis.com/problems/carddivisibility
```python
l,r = [int(x) for x in input().split()]
sum=((r*(r+1)//2)%9-(l*(l+1)//2)%9+l%9)%9
print(sum)
```

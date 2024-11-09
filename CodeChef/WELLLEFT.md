---
tags:
  - competitive-programming/judges/codechef
name: Amphibian Escape
date: 2024-07-03
---
#competitive-programming/math 
## _Solution:_
Iterate through every possible value of $A$. With some value $A$, we can calculate the number of $B$'s such that $A\cdot K+B(K-1)\ge H$. Moving the inequality around, we get that the number of $B$'s can be found with $\lfloor\frac{A\cdot K-h}{k-1}\rfloor$.

https://www.codechef.com/START141D/problems/WELLLEFT
```cpp

```
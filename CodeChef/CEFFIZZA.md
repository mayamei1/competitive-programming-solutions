---
tags:
  - competitive-programming/judges/codechef
name: Chef loves Pizza Chef loves halfs
date: 2024-07-10
---
#competitive-programming/math 
## _Solution:_
If the number of cuts are a power of $2$, then all slices are equal. If there are $x$ slices, then there must have been $\frac{x}{2}$ cuts. If we call $2^k$ the largest power of two smaller than the number of cuts, then there will be $2^k-\frac{x}{2}$ extra cuts that each would make 4 smaller slices. Thus, we get $2\cdot(2^{c}-x)$, where $2^c$ denotes the largest power of two smaller than the number of slices.

https://www.codechef.com/problems/CHEFIZZA
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd int
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

using namespace std;

void solve() {
    int x;
    cin >> x;

    int a = __lg(x);
    int b = x - (1 << a);

    cout << b * 2 << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
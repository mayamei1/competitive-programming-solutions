---
tags:
  - competitive-programming/judges/kattis
name: The Stock Market
date: 2024-10-23
---
#competitive-programming/greedy #competitive-programming/dp 
## _Solution:_
It is always optimal to either have all stocks or all money. Thus, for day $i$, we can keep track of the maximum amount of stocks and maximum amount of money that can be achieved up to that day. Say we have $dp_{i-1,m}$ and $dp_{i-1,s}$ be the max money and stocks up to day $i-1$. Then, $dp_{i,m}=\max(dp_{i-1,m},dp_{i-1,s}\cdot a_{i}-q)$ and $dp_{i,s}=\max(dp_{i-1,s},\frac{dp_{i-1,m}-q}{a_{i}})$.

https://open.kattis.com/problems/borsen
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = double;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

void solve() {
    int n;
    double q;
    cin >> n >> q;

    vi a(n);
    for (dd& x : a) cin >> x;

    double dp0 = 100, dp1 = (100 - q) / a[0];
    for (int i = 1; i < n; i++) {
        dp0 = max(dp0, dp1 * a[i] - q);
        dp1 = max(dp1, (dp0 - q) / a[i]);
    }

    printf("%.9lf\n", dp0);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Need for Speed
date: 2024-10-02
---
#competitive-programming/binary-search 
## _Solution:_
Binary search $c$. For every $m$, if all speeds are positive and the calculated time is less than the expected time, then search lower.

https://open.kattis.com/problems/speed
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
    double n, t;
    cin >> n >> t;

    vii a(n);
    for (auto& x : a) cin >> x.first >> x.second;

    double l = -1e9, h = 1e9;
    while (h - l > 1e-9) {
        double m = (h - l) / 2 + l;
        double ct = 0;
        for (auto x : a) {
            double sc = m + x.second;
            if (sc <= 0) {
                ct = 1e9;
                break;
            }
            ct += x.first / sc;
        }
        if (ct >= t) l = m;
        else h = m;
    }

    printf("%.9lf\n", l);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
---
tags:
  - competitive-programming/judges/hackerrank
name: Trampoline Triumph
date: 2024-10-28
---
#competitive-programming/binary-search 
## _Solution:_
For each range, binary search to find the maximum values for each player, then give a point to the winner of each range.

https://www.hackerrank.com/contests/lpc-2024/challenges/trampoline-triumph
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

double g(double x, double f) {
    return (6 - 2 * f * sin(x / 2) - 2 * f * sin(x / 5) - 2 * f * sin(x / 7)) * (0.9 + (1 + sin(x * f / 3)) / 20);
}

double bs(double f, double l, double r) {
    while (r - l >= 1e-9) {
        double m1 = (r - l) / 3.0 + l;
        double m2 = 2.0 * (r - l) / 3.0 + l;
        double a1 = g(m1, f);
        double a2 = g(m2, f);

        if (a1 < a2) l = m1;
        else r = m2;
    }
    return g(l, f);
}

void solve() {
    int n;
    cin >> n;

    vi f(n);
    for (dd& x : f) cin >> x;

    int m;
    cin >> m;

    vector<pair<int,int>> ans(n);
    for (int i = 0; i < n; i++) {
        ans[i].second = i + 1;
    }
    for (int i = 0; i < m; i++) {
        double l, r;
        cin >> l >> r;
        double mx = bs(f[0], l, r);
        int idx = 0;
        for (int j = 1; j < n; j++) {
            double o = bs(f[j], l, r);
            if (o > mx) mx = o, idx = j;
        }
        ans[idx].first--;
    }

    sort(ans.begin(), ans.end());
    for (auto x : ans) {
        cout << x.second << ' ' << -x.first << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/hackerrank
name: Athlete Area Allocation
date: 2024-10-26
---
#competitive-programming/complete-search 
## _Solution:_
Try every pair of points. It can also be done with divide-and-conquer.

https://www.hackerrank.com/contests/lpc-2024/challenges/athlete-area-allocation
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

double dist(dd a, dd b) {
    return sqrt(a * a + b * b);
}

void solve() {
    int n;
    cin >> n;

    vii a(n);
    for (ii& x : a) cin >> x.first >> x.second;

    double mn = 1e18;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            mn = min(mn, dist(a[i].first - a[j].first, a[i].second - a[j].second));
        }
    }

    printf("%.3lf\n", mn);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Above Average
date: 2024-09-16
---
#competitive-programming/trivial #competitive-programming/math 
## _Solution:_
Find average and count number of elements strictly greater than average.

https://open.kattis.com/problems/aboveaverage
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = int;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

void solve() {
    int n;
    cin >> n;

    vi a(n);
    for (int& x : a) cin >> x;

    int sum = 0;
    for (int x : a) {
        sum += x;
    }

    int cnt = 0;
    for (int x : a) {
        if (x * n > sum) cnt++;
    }

    printf("%.3lf%%\n", 100.0 * cnt / n);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
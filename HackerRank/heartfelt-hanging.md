---
tags:
  - competitive-programming/judges/hackerrank
name: Heartfelt Hanging
date: 2024-10-26
---
#competitive-programming/dp/classical 
## _Solution:_
Classic Knapsack problem.

https://www.hackerrank.com/contests/lpc-2024/challenges/heartfelt-hanging
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
    int k, n;
    cin >> k >> n;

    vii a(n);
    for (ii& x : a) cin >> x.first;
    for (ii& x : a) cin >> x.second;

    vvi dp(n, vi(k + 1));
    for (int j = a[0].first; j <= k; j++) {
        dp[0][j] = a[0].second;
    }

    for (int i = 1; i < n; i++) {
        for (int j = 0; j <= k; j++) {
            dp[i][j] = dp[i - 1][j];
            if (j - a[i].first >= 0) dp[i][j] = max(dp[i][j], dp[i - 1][j - a[i].first] + a[i].second);
        }
    }

    cout << dp[n - 1][k] << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
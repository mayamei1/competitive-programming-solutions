---
tags:
  - competitive-programming/judges/kattis
name: Rhythm Flow
date: 2024-10-05
---
#competitive-programming/dp 
## _Solution:_
We can solve for the answer via a two state DP table. Iterate through each button press $i$, and we keep track of the max score if we consider notes up to $j$. For a $(i,j)$, we can consider press $i$ hitting note $j$, giving us $score(i,j)+dp_{i-1,j-1}$. We can also consider if it is better for press $i$ to hit an earlier note, giving us $dp_{i,j-1}$. We can finally consider if it is better for earlier presses to hit note $j$, giving us $dp_{i-1,j}$. We set $dp_{i,j}$ to be the maximum across those values. Then, the answer is the maximum across $dp_{n,j}$ for all $1\le j\le m$.

https://open.kattis.com/problems/rhythmflow
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

vi a, b;
int score(int i, int j) {
    int diff = abs(b[i] - a[j]);
    if (diff < 16) return 7;
    if (diff < 24) return 6;
    if (diff < 44) return 4;
    if (diff < 103) return 2;
    return 0;
}

void chmax(int& val, int o) {
    val = max(val, o);
}

void solve() {
    int n, m;
    cin >> n >> m;

    a = vi(n);
    for (int& x : a) cin >> x;

    b = vi(m);
    for (int& x : b) cin >> x;

    vvi dp(m, vi(n));
    for (int j = 0; j < n; j++) {
        dp[0][j] = score(0, j);
        if (j) chmax(dp[0][j], dp[0][j - 1]);
    }

    for (int i = 1; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (j) {
                dp[i][j] = score(i, j) + dp[i - 1][j - 1];
                chmax(dp[i][j], dp[i][j - 1]);
                chmax(dp[i][j], dp[i - 1][j]);
            } else {
                dp[i][j] = score(i, j);
                chmax(dp[i][j], dp[i - 1][j]);
            }
        }
    }

    int mx = 0;
    for (int j = 0; j < n; j++) {
        chmax(mx, dp[m - 1][j]);
    }

    cout << mx << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
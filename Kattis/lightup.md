---
tags:
  - competitive-programming/judges/kattis
name: Light Up
date: 2024-10-05
---
#competitive-programming/simulation 
## _Solution:_
For each light, simulate each block that it would light up. Doing so, you can find if any two lights shine on each other and check if every open cell is lit. Then, for each blocked cell, count the number of adjacent cells with lights.

https://naq24.kattis.com/contests/naq24/problems/lightup
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

int n;
vector<string> g;
bool check(int i, int j) {
    if (i < 0 || i >= n) return 0;
    if (j < 0 || j >= n) return 0;
    return g[i][j] == '?';
}

void solve() {
    cin >> n;

    g = vector<string>(n);
    for (auto& x : g) cin >> x;

    vvi val(n, vi(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (g[i][j] != '?') continue;
            for (int k = i + 1; k < n; k++) {
                if (g[k][j] != '.') break;
                val[k][j]++;
            }
            for (int k = i - 1; k >= 0; k--) {
                val[k][j]++;
                if (g[k][j] != '.') break;
            }
            for (int k = j + 1; k < n; k++) {
                val[i][k]++;
                if (g[i][k] != '.') break;
            }
            for (int k = j - 1; k >= 0; k--) {
                val[i][k]++;
                if (g[i][k] != '.') break;
            }
        }
    }

    bool flag = true;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (g[i][j] == '?' && val[i][j] != 0) flag = false;
            if (g[i][j] == '.' && val[i][j] == 0) flag = false;
            if ('0' <= g[i][j] && g[i][j] <= '4') {
                int cnt = check(i - 1, j) + check(i + 1, j) + check(i, j - 1) + check(i, j + 1);
                if (cnt != (g[i][j] - '0')) flag = false;
            }
        }
    }

    cout << flag << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
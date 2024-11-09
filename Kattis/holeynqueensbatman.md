---
tags:
  - competitive-programming/judges/kattis
name: Holey N-Queens (Batman)
date: 2024-09-23
---
#competitive-programming/complete-search
## _Solution:_
Classic 8 queens problem, but there are now invalid spots. Perform complete search by starting on the first row and setting a queen in a column, then recursively setting a queen in the row below. Checking collisions can be done in constant time by keeping track of an boolean array to denote visited columns, or visited $i+j$ diagonals, or visited $i-j$ diagonals.

https://open.kattis.com/problems/holeynqueensbatman
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

int n, m;
vi col;
vi d1;
vi d2;
set<ii> hole;

ll dfs(int i) {
    if (i == n) return 1;
    ll sum = 0;
    for (int j = 0; j < n; j++) {
        if (col[j] || d1[i + j] || d2[i - j + n] || hole.count({i, j})) continue;
        col[j] = 1;
        d1[i + j] = 1;
        d2[i - j + n] = 1;
        sum += dfs(i + 1);
        col[j] = 0;
        d1[i + j] = 0;
        d2[i - j + n] = 0;
    }
    return sum;
}

void solve() {
    col = vi(n);
    d1 = vi(2 * n + 2);
    d2 = vi(2 * n + 2);
    hole.clear();

    for (int i = 0; i < m; i++) {
        int x, y;
        cin >> x >> y;
        hole.insert({x, y});
    }

    cout << dfs(0) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n >> m && !(n == 0 && m == 0)) solve();
}
```
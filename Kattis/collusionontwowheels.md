---
tags:
  - competitive-programming/judges/kattis
name: Collusion on Two Wheels
date: 2023-02-22
---
#competitive-programming/binary-search #competitive-programming/graph/bipartite 
## _Solution:_
Binary search $m$, and for a fixed $m$, only consider edges greater than $m$. Then, we can check if the graph can be bipartite, and if it is, then this is a valid $m$.

https://open.kattis.com/problems/collusionontwowheels
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
vvi adj;

vi c;
bool dfs(int u, bool val, int req) {
    if (c[u] != -1) return c[u] == val;
    c[u] = val;

    for (int v = 0; v < n; v++) {
        if (adj[u][v] > req && !dfs(v, !val, req)) return false;
    }

    return true;
}

void solve() {
    cin >> n;

    vii a(n);
    for (ii& x : a) cin >> x.first >> x.second;

    adj = vvi(n, vi(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            adj[i][j] = abs(a[i].first - a[j].first) + abs(a[i].second - a[j].second);
        }
    }

    int l = -1, h = 2000;
    while (h - l > 1) {
        int m = (h - l) / 2 + l;
        
        c = vi(n, -1);
        bool flag = true;
        for (int i = 0; i < n; i++) {
            if (c[i] == -1 && !dfs(i, 0, m)) flag = false;
        }

        if (flag) h = m;
        else l = m;
    }

    cout << h << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
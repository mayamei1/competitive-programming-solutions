---
tags:
  - competitive-programming/judges/kattis
name: Gopher II
date: 2024-10-08
---
#competitive-programming/graph/bipartite/maximum-matching
## _Solution:_
Calculate the maximum allowed distance, then create edges between gophers and holes that are at most that distance away. Then perform maximum bipartite matching and count the number of matches.

https://open.kattis.com/problems/gopher2
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

int n, m, s, v;

ll dist(ll a, ll b) {
    return a * a + b * b;
}

vvi adj;
vi vis;
vi mt;

bool dfs(int u) {
    if (vis[u]) return false;
    vis[u] = true;

    for (int v : adj[u]) {
        if (mt[v] == -1 || dfs(mt[v])) {
            mt[v] = u;
            return true;
        }
    }

    return false;
}

void solve() {
    v *= 10;

    vii a(n);
    for (ii& x : a) {
        double a, b;
        cin >> a >> b;
        x.first = a * 10 + 0.5, x.second = b * 10 + 0.5;
    }

    vii b(m);
    for (ii& x : b) {
        double a, b;
        cin >> a >> b;
        x.first = a * 10 + 0.5, x.second = b * 10 + 0.5;
    }

    adj = vvi(n);

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            ll x = dist(a[i].first - b[j].first, a[i].second - b[j].second);
            ll y = 1ll * v * v * s * s;
            if (x <= y) adj[i].push_back(j);
        }
    }

    mt = vi(m, -1);
    int ans = 0;
    for (int i = 0; i < n; i++) {
        vis = vi(n);
        if (dfs(i)) ans++;
    }

    cout << n - ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n >> m >> s >> v) solve();
}
```
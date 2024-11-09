---
tags:
  - competitive-programming/judges/kattis
name: Elementary Math
date: 2024-10-08
---
#competitive-programming/graph/bipartite/maximum-matching 
## _Solution:_
Create edges between each pair of numbers and the possible answers, then perform maximum bipartite matching.

https://open.kattis.com/problems/elementarymath
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = ll;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

vvi adj;
vi vis;
map<ll, int> mt;

bool dfs(int u) {
    if (vis[u]) return false;
    vis[u] = true;

    for (ll v : adj[u]) {
        if (mt.count(v) == 0 || dfs(mt[v])) {
            mt[v] = u;
            return true;
        }
    }

    return false;
}

void solve() {
    int n;
    cin >> n;

    vvi ans(n);
    adj = vvi(n);
    for (int i = 0; i < n; i++) {
        ll a, b;
        cin >> a >> b;

        ans[i] = {a, b, 0};

        adj[i].push_back(a + b);
        adj[i].push_back(a - b);
        adj[i].push_back(a * b);
    }

    
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        vis = vi(n);
        if (dfs(i)) cnt++;
    }

    if (cnt != n) {
        cout << "impossible" << endl;
        return;
    } 

    for (auto [a, u] : mt) {
        ans[u][2] = a;
    }

    for (int i = 0; i < n; i++) {
        ll a = ans[i][0], b = ans[i][1], c = ans[i][2];
        char op;
        if (a + b == c) op = '+';
        else if (a - b == c) op = '-';
        else op = '*';
        printf("%lld %c %lld = %lld\n", a, op, b, c);
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
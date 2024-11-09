---
tags:
  - competitive-programming/judges/kattis
name: Breaking Bad
date: 2024-10-07
---
#competitive-programming/graph/bipartite #competitive-programming/graph/dfs 
## _Solution:_
Simple bipartite check.

https://open.kattis.com/problems/breakingbad
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

vvi adj;
vi ans;

bool dfs(int u, bool val) {
    if (ans[u] != -1) return ans[u] == val;
    ans[u] = val;

    for (int v : adj[u]) {
        if (!dfs(v, !val)) return false;
    }

    return true;
}

void solve() {
    int n;
    cin >> n;

    map<string, int> id;
    vector<string> rev(n);
    for (int i = 0; i < n; i++) {
        string s;
        cin >> s;

        id[s] = i;
        rev[i] = s;
    }

    adj = vvi(n);
    ans = vi(n, -1);

    int m;
    cin >> m;

    for (int i = 0; i < m; i++) {
        string su, sv;
        cin >> su >> sv;
        adj[id[su]].push_back(id[sv]);
        adj[id[sv]].push_back(id[su]);
    }

    bool a = 1;
    for (int i = 0; i < n; i++) {
        if (ans[i] == -1 && !dfs(i, 0)) a = 0;
    }

    if (!a) {
        cout << "impossible" << endl;
        return;
    }

    for (int i = 0; i < n; i++) {
        if (ans[i] == 0) cout << rev[i] << ' ';
    }
    cout << endl;
    for (int i = 0; i < n; i++) {
        if (ans[i] == 1) cout << rev[i] << ' ';
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
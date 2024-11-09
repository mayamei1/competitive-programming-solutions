---
tags:
  - competitive-programming/judges/kattis
name: Longest path in a DAG
date: 2024-08-28
---
#competitive-programming/graph/dag #competitive-programming/graph/dfs #competitive-programming/dp 
## _Solution:_
Use DFS/DP to keep track of the longest path from any vertex. For some vertex $v$, the longest path is the maximum longest path of its children plus one.

https://open.kattis.com/problems/longestpathinadag
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
vii memo;
ii dfs(int u) {
    if (memo[u].first != -1) return memo[u];
    ii ans {0, -1};

    for (int v : adj[u]) {
        ii t = dfs(v);
        if (t.first > ans.first) ans = {t.first, v};
    }
    ans.first++;
    memo[u] = ans;
    return ans;
}

void solve() {
    int n, m;
    cin >> n >> m;

    adj = vvi(n + 1);
    memo = vii(n + 1, {-1, -1});
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
    }

    
    int r = 0;
    for (int i = 1; i <= n; i++) {
        ii t = dfs(i);
        if (t.first > memo[r].first) r = i;
    }

    cout << memo[r].first << endl;
    while (r != -1) {
        cout << r << ' ';
        r = memo[r].second;
    }

    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
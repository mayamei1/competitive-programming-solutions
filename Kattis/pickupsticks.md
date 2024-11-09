---
tags:
  - competitive-programming/judges/kattis
name: Pick up sticks
date: 2023-02-04
---
#competitive-programming/graph/dag #competitive-programming/graph/scc #competitive-programming/graph/dfs 
## _Solution:_
Find topological order, and detect if a cycle exists.

https://open.kattis.com/problems/pickupsticks
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

bool dfs(vvi& adj, vi& vis, vi& sorted, int u) {
    if (vis[u] == 1) return 0;
    if (vis[u] == 2) return 1;
    vis[u] = 2;

    for (int v : adj[u]) {
        if (dfs(adj, vis, sorted, v)) return 1;
    }

    vis[u] = 1;
    sorted.push_back(u);
    return 0;
}

// returns empty list if not DAG
vi topological_sort(vvi& adj) {
    int n = adj.size();
    vi visited(n);
    vi sorted;

    for (int i = 0; i < n; i++) {
        if (!visited[i] && dfs(adj, visited, sorted, i)) return vi();
    }
    reverse(sorted.begin(), sorted.end());
    return sorted;
}

void solve() {
    int n, m;
    cin >> n >> m;

    vvi adj(n + 1);

    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;

        adj[u].push_back(v);
    }

    vi ans = topological_sort(adj);
    if (ans.size() == 0) {
        cout << "IMPOSSIBLE" << endl;
        return;
    }
    for (int a : ans) {
        if (a == 0) continue;
        cout << a << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/atcoder
name: Shortest Path  3
date: 2024-07-12
---
#competitive-programming/graph/dijkstra #competitive-programming/graph/sssp #competitive-programming/graph/weighted 
## _Solution:_
Apply Dijkstra's algorithm. The directed edges can be generated by taking the bidirectional edge with weight $B_j$, and converting it to two directed edges with the weights as $B_j$ plus the weight of the destination vertex.

https://atcoder.jp/contests/abc362/tasks/abc362_d
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd ll
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

using namespace std;

const int N = 2e5 + 2;
ll a[N];
vii adj[N];
ll dist[N];

void solve() {
    int n, m;
    cin >> n >> m;

    memset(dist, -1, sizeof(dist));

    for (int i = 1; i <= n; i++) cin >> a[i];
    
    for (int i = 0; i < m; i++) {
        ll u, v, b;
        cin >> u >> v >> b;

        adj[u].push_back({b + a[v], v});
        adj[v].push_back({b + a[u], u});
    }

    priority_queue<ii, vii, greater<>> pq;
    pq.push({a[1], 1});

    while (!pq.empty()) {
        ll d, u;
        tie(d, u) = pq.top(); pq.pop();

        if (dist[u] != -1) continue;
        dist[u] = d;

        for (auto [c, v] : adj[u]) {
            pq.push({d + c, v});
        }
    }

    for (int i = 2; i <= n; i++) {
        cout << dist[i] << ' ';
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
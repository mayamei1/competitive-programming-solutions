---
tags:
  - competitive-programming/judges/hackerrank
name: Bouncy Castle Obstacle Course
date: 2024-10-26
---
#competitive-programming/graph/dijkstra #competitive-programming/graph/sssp #competitive-programming/graph/weighted
## _Solution:_
Dijkstra's algorithm, but the edges add an additional $\lfloor \frac{d}{10}\rfloor$ weight, where $d$ is minimum distance to the current vertex $v$.

https://www.hackerrank.com/contests/lpc-2024/challenges/bouncy-castle-obstacle-course
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

struct comp_pair {
    template <class T1, class T2>
    bool operator()(const pair<T1, T2>& a, const pair<T1, T2>& b) const {
        return a.second > b.second;
    }
};

#define INF -1

void solve() {
    int n;
    cin >> n;

    vvii adj(n);

    map<string, int> idx;
    for (int i = 0; i < n; i++) {
        string s;
        cin >> s;
        idx[s] = i;
    }

    int m;
    cin >> m;
    for (int i = 0; i < m; i++) {
        string u, v;
        int w;
        cin >> u >> v >> w;
        adj[idx[u]].push_back({idx[v], w});
        adj[idx[v]].push_back({idx[u], w});
    }

    vi dist(n, INF);
    priority_queue<ii, vii, comp_pair> q;
    q.push({0, 0});
    while (!q.empty()) {
        ii c = q.top(); q.pop();
        int v = c.first, d = c.second;

        if (dist[v] != INF) continue;
        dist[v] = d;

        for (ii e: adj[v]) {
            q.push({e.first, d + e.second + d / 10});
        }
    }

    cout << dist[n - 1] << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Water
date: 2024-06-23
---
#competitive-programming/graph/max-flow #competitive-programming/graph/bfs 
## _Solution:_
With initial graph, perform max flow. Then, with each improvement, be sure to add to the capacity of edge $(a,b)$ and ensure that $(a,b)$ is in the adjacency matrix, then rerun the max flow, keeping the same residual capacities from previous runs.

https://open.kattis.com/problems/water
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd int
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

const int N = 100 + 2;
int INF = -1;
int capacity[N][N];
set<int> adj[N];
int parent[N];

int n, s, t, p, k;

int bfs() {
    fill(parent, parent + n + 1, -1);
    parent[s] = -2;
    queue<ii> q;
    q.push({s, INF});

    while (!q.empty()) {
        int u, f, nf;
        tie(u, f) = q.front(); q.pop();

        for (int v : adj[u]) {
            if (parent[v] == -1 && capacity[u][v]) {
                parent[v] = u;
                if (f == INF) nf = capacity[u][v];
                else nf = min(f, capacity[u][v]);
                if (v == t) return nf;
                q.push({v, nf});
            }
        }
    }

    return 0;
}

int maxflow() {
    int flow = 0, nflow;

    while (nflow = bfs()) {
        flow += nflow;
        int v = t;
        while (v != s) {
            int u = parent[v];
            capacity[u][v] -= nflow;
            capacity[v][u] += nflow;
            v = u;
        }
    }

    return flow;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n >> p >> k;
    s = 1, t = 2;

    for (int i = 0; i < p; i++) {
        int a, b, c;
        cin >> a >> b >> c;
        adj[a].insert(b);
        adj[b].insert(a);
        capacity[a][b] = c;
        capacity[b][a] = c;
    }

    int flow = maxflow();
    cout << flow << endl;
    for (int i = 0; i < k; i++) {
        int a, b, c;
        cin >> a >> b >> c;
        adj[a].insert(b);
        adj[b].insert(a);
        capacity[a][b] += c;
        capacity[b][a] += c;
        flow += maxflow();
        cout << flow << endl;
    }
}
```
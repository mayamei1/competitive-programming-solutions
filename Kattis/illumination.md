---
tags:
  - competitive-programming/judges/kattis
name: Illumination
date: 2024-06-22
---
#competitive-programming/graph/2-sat #competitive-programming/graph/scc #competitive-programming/graph/dfs 
## _Solution:_
If two points share the same value in one dimension, and are at most $r$ away from each other, then they can not be oriented in dimension that they share. This can be represented as a 2-SAT problem. If two points can not be oriented vertically, we can represent it in CNF form as $p_{i}\cup p_{j}$ (or if $p_i$ and $p_j$ are both 0, then the condition fails). Likewise, we can represent not being able to orient horizontally as $-p_{i}\cup-p_{j}$ (or if $p_i$ and $p_j$ are both 1, the condition fails).

https://open.kattis.com/problems/illumination
```cpp
#include <bits/stdc++.h>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll

using namespace std;

vvi adj, rev_adj;
vi vis;
vi order;

void dfs1(int v) {
    vis[v] = 1;
    for (int u : adj[v])
        if (!vis[u])
            dfs1(u);
    order.push_back(v);
}

void dfs2(int v, int t) {
    vis[v] = t;
    for (int u : rev_adj[v])
        if (!vis[u])
            dfs2(u, t);
}

bool comp(int x1, int x2, int r) {
    if ((x1 - r) <= (x2 - r) && (x2 - r) <= (x1 + r)) return true;
    if ((x1 - r) <= (x2 + r) && (x2 + r) <= (x1 + r)) return true;
    return false;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, r, k;
    cin >> n >> r >> k;

    vii lamps(k);
    for (int i = 0; i < k; i++) {
        cin >> lamps[i].first >> lamps[i].second;
    }

    adj = vvi(2 * k);
    rev_adj = vvi(2 * k);
    vis = vi(2 * k);

    for (int i = 0; i < k; i++) {
        for (int j = i + 1; j < k; j++) {
            int lix, liy, ljx, ljy;
            tie(lix, liy) = lamps[i];
            tie(ljx, ljy) = lamps[j];
            if (liy == ljy && comp(lix, ljx, r)) {
                int u = 2 * i + 1, v = 2 * j + 1;
                int nu = 2 * i, nv = 2 * j;
                adj[nu].push_back(v);
                adj[nv].push_back(u);
                rev_adj[v].push_back(nu);
                rev_adj[u].push_back(nv);
            }
            if (lix == ljx && comp(liy, ljy, r)) {
                int u = 2 * i, v = 2 * j;
                int nu = 2 * i + 1, nv = 2 * j + 1;
                adj[nu].push_back(v);
                adj[nv].push_back(u);
                rev_adj[v].push_back(nu);
                rev_adj[u].push_back(nv);
            }
        }
    }

    for (int i = 0; i < (2 * k); i++)
        if (!vis[i])
            dfs1(i);
    vis.assign(2 * k, 0);
    reverse(order.begin(), order.end());

    int t = 1;
    for (auto i : order) {
        if (!vis[i]) {
            dfs2(i, t);
            t++;
        }
    }
    
    for (int i = 0; i < (2 * k); i += 2) {
        if (vis[i] == vis[i + 1]) {
            cout << 0 << endl;
            return 0;
        }
    }
    cout << 1 << endl;
}
```
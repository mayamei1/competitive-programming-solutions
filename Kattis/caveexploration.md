---
tags:
  - competitive-programming/catalog/kattis
name: Cave Exploration
---
#competitive-programming/graph/bridges #competitive-programming/graph/dfs 
## _Solution:_
DFS to find bridges. DFS again to count the number of vertices that you can reach without going through bridges.

https://open.kattis.com/problems/caveexploration
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <list>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>
#include <bitset>
#include <iomanip>

#define ll long long int
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

vi tin, low, visited;
vvi adj;
int timer;

set<ii> inv;
void dfs1(int v, int p = -1) {
    visited[v] = 1;
    tin[v] = low[v] = timer++;

    for (int to : adj[v]) {
        if (to == p) continue;
        if (visited[to]) {
            low[v] = min(low[v], tin[to]);
        } else {
            dfs1(to, v);
            low[v] = min(low[v], low[to]);

            if (low[to] > tin[v]) {
                inv.insert({v, to});
                inv.insert({to, v});
            }
        }
    }
}

int dfs2(int v) {
    int ans = 1;
    visited[v] = 1;
    for (int to : adj[v]) {
        if (visited[to]) continue;
        if (inv.find({v, to}) != inv.end()) continue;
        ans += dfs2(to);
    }
    return ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    cin >> n >> m;

    tin = vi(n, -1);
    low = vi(n, -1);
    visited = vi(n, 0);
    adj = vvi(n);
    timer = 0;

    f (i, 0, m) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    dfs1(0);
    visited = vi(n, 0);
    cout << dfs2(0) << endl;
}
```
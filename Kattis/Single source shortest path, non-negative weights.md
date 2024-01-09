---
type:
  - competitive-programming
  - kattis
tags:
  - graph/dijkstra
  - graph/sssp
  - graph/weighted
---
#kattis #kattis-shortestpath1

## _Solution:_
Use Dijkstra's algorithm. There can be multiple directed edges with the same source/destination pair.

https://open.kattis.com/problems/shortestpath1
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

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll
#define vs vector<string>

#define umap unordered_map
#define uset unordered_set

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

#define LSOne(S) ((S) & -(S))
#define INF -1

struct comp_pair {
    template <class T1, class T2>
    bool operator()(const pair<T1, T2>& a, const pair<T1, T2>& b) const {
        return a.second > b.second;
    }
};

int n, m, q, s;
vvii edges;
vi dist;

void precalc() {
    dist = vi(n, INF);

    priority_queue<ii, vii, comp_pair> q;
    q.push({s, 0});

    while (!q.empty()) {
        ii c = q.top(); q.pop();
        int v = c.first, d = c.second;

        if(dist[v] != INF) continue;
        dist[v] = d;

        for (ii e : edges[v]) {
            q.push({e.first, d + e.second});
        }
    }
}

void solve(int u) {
    if (dist[u] == INF) cout << "Impossible\n";
    else cout << dist[u] << '\n';
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n >> m >> q >> s) {
        if(n == 0 && m == 0 && q == 0 && s == 0) break;

        edges = vvii(n);
        f (i, 0, m) {
            int u, v, w;
            cin >> u >> v >> w;
            edges[u].push_back({v, w});
        }        

        precalc();

        f (i, 0, q) {
            int u;
            cin >> u;
            solve(u);
        }
    }
}
```
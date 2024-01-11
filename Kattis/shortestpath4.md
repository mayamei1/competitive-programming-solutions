---
type:
  - competitive-programming
  - kattis
tags:
  - graph/dijkstra
  - graph/sssp
  - "#graph/weighted"
  - graph/state-space
name: Single source shortest path, safe path
---
## _Solution:_
Dijkstra's algorithm, but the state space includes a dimension for current number of junctions. Make sure to not push next edges if the current number of junctions is already at $k$. If at any point you reach the destination, terminate early and print answer.

https://open.kattis.com/problems/shortestpath4
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

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

int tc, v, x, q, s, t, k;

#define INF -1

struct iii {
    int v, m, d;
};

struct comp {
    bool operator()(const iii& a, const iii& b) const {
        return a.d > b.d;
    }
};

vvii edges; // get from input as adj list of ii = {vertex, weight}
vvi dist; // dist of every vertex from vertex 's'

int precalc() {
    dist = vvi(v, vi(k + 1, INF));

    priority_queue<iii, vector<iii>, comp> q;
    q.push({s, 1, 0});

    while (!q.empty()) {
        iii c = q.top(); q.pop();

        if (c.v == t) return c.d;
        if (dist[c.v][c.m] != INF) continue;
        dist[c.v][c.m] = c.d;

        if (c.m == k) continue;

        for (ii e : edges[c.v]) {
            q.push({e.first, c.m + 1, c.d + e.second});
        }
    }

    return INF;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> tc;
    while (tc--) {
        cin >> v;
        edges = vvii(v);
        f (i, 0, v) {
            cin >> x;
            edges[i] = vii(x);
            f (j, 0, x) {
                cin >> edges[i][j].first >> edges[i][j].second;
            }        
        }

        cin >> q;
        f (i, 0, q) {
            cin >> s >> t >> k;
            cout << precalc() << '\n';
        }
        cout << '\n';
    }
}
```
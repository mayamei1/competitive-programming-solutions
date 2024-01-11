---
type:
  - competitive-programming
  - kattis
tags:
  - graph/dijkstra
  - graph/sssp
  - graph/weighted
name: Bridges
---
## _Solution:_
Use Dijkstra's algorithm, with the $c$ value of each edge as the weight.

https://open.kattis.com/problems/bryr
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
#define INF -1 // TODO SET TO VERY HIGH VALUE

struct comp_pair {
    template <class T1, class T2>
    bool operator()(const pair<T1, T2>& a, const pair<T1, T2>& b) const {
        return a.second > b.second;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m; // number of vertices
    cin >> n >> m;
    vvii edges(n); // {vertex, distance}
    int a, b, c;
    f (i, 0, m) {
        cin >> a >> b >> c;
        a--;
        b--;
        edges[a].push_back({b, c});
        edges[b].push_back({a, c});
    }

    vi dist(n);
    f (i, 0, n) {
        dist[i] = INF;
    }

    priority_queue<ii, vii, comp_pair> q;
    q.push({0, 0});

    while (!q.empty()) {
        ii c = q.top(); q.pop();
        int v = c.first, d = c.second;

        if(dist[v] != INF) continue;
        dist[v] = d;
        
        for (ii e : edges[v]) {
            q.push({e.first, d + e.second});
        }
    }

    cout << dist[n - 1];
}
```
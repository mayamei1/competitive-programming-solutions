---
tags:
  - competitive-programming/catalog/kattis
name: Trapezoid Walkway
---
#competitive-programming/graph/dijkstra
#competitive-programming/graph/sssp
#competitive-programming/graph/weighted
## _Solution:_
Do Dijkstra's algorithm, where the vertices are widths, and the trapezoids represent an edge with the $\mathrm{area}\times2$ as the weight.

https://open.kattis.com/problems/walkway
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

int n, s;
vvii edges; // get from input as adj list of ii = {vertex, weight}
vi dist; // dist of every vertex from vertex 's'

void precalc() {
    dist = vi(1001, INF);

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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n && n) {
        edges = vvii(1001);
        int a, b, h;
        f (i, 0, n) {
            cin >> a >> b >> h;
            int d = (a + b) * h;
            edges[a].push_back({b, d});
            edges[b].push_back({a, d});
        }

        int t;
        cin >> s >> t;

        precalc();
        cout << (dist[t] / 100.0) << '\n';
    }
}
```
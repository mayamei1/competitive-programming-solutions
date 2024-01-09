---
type:
  - competitive-programming
  - kattis
tags:
  - graph/dijkstra
  - graph/sssp
  - graph/weighted
  - graph/state-space
---
#kattis #kattis-nikola

## _Solution:_
Vertices represent the current square and jump (max jump value is $N-1$). There are up to two edges (going to `(curr_sq+jump+1, curr_jump+1)` or `(curr_sq-jump, jump)`) and the weights are the fees of the destination square. Use Dijkstra's algorithm and the answer is the minimum "distance" at vertex $N$ with any jump value.

https://open.kattis.com/problems/nikola
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
struct iii {
    int v, j, d;
};

struct comp_pair {
    bool operator()(const iii& a, const iii& b) const {
        return a.d > b.d;
    }
};

int n;
vi w;
vvi dist; // dist of every vertex from vertex 's'

void precalc() {
    dist = vvi(n, vi(n, INF));

    priority_queue<iii, vector<iii>, comp_pair> q;
    q.push({0, 0, 0});

    while (!q.empty()) {
        iii c = q.top(); q.pop();
        int v = c.v, j = c.j, d = c.d;
        
        if (v < 0 || v >= n) continue;
        if(dist[v][j] != INF) continue;
        dist[v][j] = d;

        q.push({v + j + 1, j + 1, d + w[v + j + 1]});
        q.push({v - j, j, d + w[v - j]});
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;

    w = vi(n);
    f (i, 0, n) {
        cin >> w[i];
    }

    precalc();

    int mn = 10000000;
    f (i, 0, n) {
        if (dist[n - 1][i] != -1) mn = min(mn, dist[n - 1][i]);
    }

    cout << mn;
}
```
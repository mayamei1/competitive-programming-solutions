---
type:
  - competitive-programming
  - kattis
tags:
  - graph/dijkstra
  - graph/sssp
  - "#graph/weighted"
name: Human Cannonball Run
---
## _Solution:_
Calculate edges with vertices as the start/stop locations and the cannon locations. Start doesn't have the option to "launch" and stop doesn't have any edges going out. Use Dijkstra's algorithm.

https://open.kattis.com/problems/humancannonball
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
#define id pair<int, double>

struct comp_pair {
    template <class T1, class T2>
    bool operator()(const pair<T1, T2>& a, const pair<T1, T2>& b) const {
        return a.second > b.second;
    }
};

int n, s;
vector<vector<id>> edges; // get from input as adj list of ii = {vertex, weight}
vector<double> dist; // dist of every vertex from vertex 's'

void precalc() {
    dist = vector<double>(n, INF);

    priority_queue<id, vector<id>, comp_pair> q;
    q.push({s, 0});

    while (!q.empty()) {
        id c = q.top(); q.pop();
        int v = c.first;
        double d = c.second;

        if(dist[v] != INF) continue;
        dist[v] = d;

        for (id e : edges[v]) {
            q.push({e.first, d + e.second});
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    double ax, ay, bx, by;
    cin >> ax >> ay >> bx >> by;

    vector<pair<double, double>> p;
    p.push_back({ax, ay});
    p.push_back({bx, by});

    cin >> n;
    f (i, 0, n) {
        cin >> ax >> ay;
        p.push_back({ax, ay});
    }

    n = p.size();
    edges = vector<vector<id>>(n);
    f (i, 0, n) {
        f (j, 0, n) {
            if (i == j) continue;
            double dx = p[i].first - p[j].first;
            double dy = p[i].second - p[j].second;
            double d = sqrt(dx * dx + dy * dy);

            if (i == 0) {
                edges[i].push_back({j, d / 5});
            } else if (i == 1) {
                continue;
            } else {
                double c_d = fabs(d - 50);
                edges[i].push_back({j, min(d / 5, 2 + c_d / 5)});
            }
        }
    }

    s = 0;
    precalc();

    printf("%0.8lf", dist[1]);
}
```
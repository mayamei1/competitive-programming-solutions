---
tags:
  - competitive-programming/judges/kattis
name: Self-Assembly
date: 2024-01-23
---
#competitive-programming/problem-reduction
#competitive-programming/graph/cycle-detection
#competitive-programming/graph/dfs
## _Solution:_
First, assume we can find an unbounded structure, however, there can be one or more "collisions" or intersections. Convince yourself that this structure can be simplified to a path. Since we are allowed to reflect/flip molecules, we can "flip" angles of the path. Observe that this path can then be transformed to be a staircase-shape (or sometimes a straight line), which does not have any intersections. This proves that the "geometry" of the path ultimately does not matter.

To find if a structure is unbound, you can try to find some sort of cycle. However, instead of trying to build up structures and testing if they are a cycle, you can transform the graph, so that the vertices are no longer the molecules, but rather the faces (A+, A-, etc.) of the molecule. The edges are now the opposite of the faces that of the same molecule. Example, if you have "00B+D+A-," then the "B+" face will have edges to "D-" and "A+."

Finally, observe that we can merge faces with the same letters (A+ with A+, A- with A-) to the same vertex. In the end, we have a directed graph, which allows us to do cycle detection.

https://open.kattis.com/problems/assembly
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

int n;

vvi adj;
vi visited;

bool dfs(int v) {
    if (visited[v] == 2) return true;
    if (visited[v] == 1) return false;
    visited[v] = 2;

    for (int u : adj[v]) {
        if (dfs(u)) return true;
    }

    visited[v] = 1;
    return false;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;
    string s;
    adj = vvi(2 * 26);
    visited = vi(2 * 26);
    f (i, 0, n) {
        cin >> s;
        vi ids;
        f (j, 0, 4) {
            string l = s.substr(2 * j, 2);
            if (l == "00") continue;
            int id = (l[0] - 'A') + 26 * (l[1] == '-');
            ids.push_back(id);
        }
        f (j, 0, ids.size()) {
            f (k, 0, ids.size()) {
                if (j == k) continue;
                int v = ids[j];
                int u = (ids[k] + 26) % (2 * 26);
                adj[v].push_back(u);
            }
        }
    }

    f (v, 0, 2 * 26) {
        if (dfs(v)) {
            cout << "unbounded";
            return 0;
        }
    }
    cout << "bounded";
}
```
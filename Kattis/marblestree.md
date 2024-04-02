---
tags:
  - competitive-programming/catalog/kattis
name: Marbles On A Tree
---
#competitive-programming/graph/tree
#competitive-programming/dp
## _Solution:_
For a particular subtree, you want to push any supply or deficit of marbles from the children up to the parent/root. Pushing deficit is like pushing extras down to the children. So, for a subtree, where the supply/deficit is pushed to its root, the number of moves can be calculated by summing up the magnitude of supply/deficit of the children.

https://open.kattis.com/problems/marblestree
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
vi m;
vvi adj;
vi visited;

ii dfs(int v) {
    visited[v] = true;

    ii curr = {0, m[v] - 1};
    for (int u : adj[v]) {
        if (!visited[u]) {
            ii val = dfs(u);
            curr.first += val.first + ((val.second > 0) ? val.second : -val.second);
            curr.second += val.second;
        }
    }

    return curr;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n && n != 0) {
        int v, d, c;
        m = vi(n);
        adj = vvi(n);
        visited = vi(n);

        f (i, 0, n) {
            cin >> v >> m[--v] >> d;
            f (j, 0, d) {
                cin >> c;
                c--;
                adj[v].push_back(c);
                adj[c].push_back(v);
            }
        }

        cout << dfs(0).first << '\n';
    }
}
```
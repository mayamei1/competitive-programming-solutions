---
type:
  - competitive-programming
  - kattis
tags:
  - graph/flood-fill
  - graph/dfs
  - graph/bfs
name: Terraces
---
## _Solution:_
Iterate through each cell, and DFS/BFS to flood-fill and find/count all cells that neighbor the initial cell that have the same value, and if at any point, any of those neighbors have a lower value, then invalidate the search.

https://open.kattis.com/problems/terraces
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

int x, y;
vvi visited, grid;

int dfs(int val, int i, int j) {
    if (i < 0 || i >= y) return 0;
    if (j < 0 || j >= x) return 0;

    if (grid[j][i] > val) return 0;
    if (grid[j][i] < val) return -1;
    if (visited[j][i]) return 0;

    visited[j][i] = 1;

    int a = dfs(val, i + 1, j);
    int b = dfs(val, i - 1, j);
    int c = dfs(val, i, j + 1);
    int d = dfs(val, i, j - 1);

    if (a == -1 || b == -1 || c == -1 || d == -1) {
        return -1;
    }

    return a + b + c + d + 1;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> x >> y;

    visited = vvi(x, vi(y, 0));
    grid = vvi(x, vi(y, 0));

    f (i, 0, y) {
        f (j, 0, x) {
            cin >> grid[j][i];
        }
    }

    int count = 0;
    f (i, 0, y) {
        f (j, 0, x) {
            int a = dfs(grid[j][i], i, j);
            if (a != -1) {
                count += a;
            }
        }
    }

    cout << count;
}
```
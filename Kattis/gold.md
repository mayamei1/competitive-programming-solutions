---
type:
  - competitive-programming
  - kattis
tags:
  - graph/dfs
  - graph/bfs
name: Getting Gold
---
## _Solution:_
DFS/BFS starting from the player's starting location. At each node, before you traverse to others, if the current node has a trap as a neighbor, do not traverse past this node.

https://open.kattis.com/problems/gold
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

int w, h;
vs grid;
vvi visited;

bool check(int i, int j) {
    if (i < 0 || i >= h) return 0;
    if (j < 0 || j >= w) return 0;
    return (grid[i][j] == 'T');
}

int dfs(int i, int j) {
    if (i < 0 || i >= h) return 0;
    if (j < 0 || j >= w) return 0;
    if (visited[i][j]) return 0;
    visited[i][j] = 1;
    if (grid[i][j] == '#') return 0;
    int sum = (grid[i][j] == 'G');
    if (check(i - 1, j) || check(i + 1, j) || check(i, j - 1) || check(i, j + 1)) return sum;
    sum += dfs(i - 1, j);
    sum += dfs(i + 1, j);
    sum += dfs(i, j - 1);
    sum += dfs(i, j + 1);
    return sum;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> w >> h;
    grid = vs(h);
    visited = vvi(h, vi(w, 0));
    int s_i, s_j;
    f (i, 0, h) {
        cin >> grid[i];
        f (j, 0, w) {
            if (grid[i][j] == 'P') {
                s_i = i; s_j = j;
            }
        }
    }

    cout << dfs(s_i, s_j);
}
```
---
tags:
  - competitive-programming/judges/ieeextreme
name: Watershed
date: 2023-10-28
---
#competitive-programming/graph/dfs
#competitive-programming/graph/flood-fill
## _Solution:_
Look for locations in the grid where there are no outgoing edges. These locations are drains and for each of them, DFS up to higher elevations to find out how much water is flowing into it. Have a separate grid to determine if a cell has already been calculated to avoid re-computations. For any particular cell that has not been calculated yet, continue to DFS up to find out how much water flows into the *current* cell. Once all of the "children" have been calculated, you can calculate your own cell. Do this until the drain is calculated. Find maximum water any drain has.

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

int n, m;
vvi h;
vector<vector<double>> w;

double dfs(int i, int j) {
    if (i < 0 || i == n) return 0;
    if (j < 0 || j == m) return 0;
    if (w[i][j] != -1) return w[i][j];

    double sum = 1; int outgoing = 0;
    if (i != 0)
        if (h[i][j] < h[i - 1][j]) sum += dfs(i - 1, j);
        else if (h[i][j] > h[i - 1][j]) outgoing++;
    if (i != n - 1)
        if (h[i][j] < h[i + 1][j]) sum += dfs(i + 1, j);
        else if (h[i][j] > h[i + 1][j]) outgoing++;
    if (j != 0)
        if (h[i][j] < h[i][j - 1]) sum += dfs(i, j - 1);
        else if (h[i][j] > h[i][j - 1]) outgoing++;
    if (j != m - 1)
        if (h[i][j] < h[i][j + 1]) sum += dfs(i, j + 1);
        else if (h[i][j] > h[i][j + 1]) outgoing++;
    w[i][j] = sum / max(1, outgoing);
    return w[i][j];
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n >> m;

    h = vvi(n, vi(m));
    w = vector<vector<double>>(n, vector<double>(m, -1));

    f (i, 0, n) {
        f (j, 0, m) {
            cin >> h[i][j];
        }
    }

    double ans = 0;
    f (i, 0, n) {
        f (j, 0, m) {
            bool is_drain = true;
            if (i != 0 && h[i][j] > h[i - 1][j]) is_drain = false;
            if (i != n - 1 && h[i][j] > h[i + 1][j]) is_drain = false;
            if (j != 0 && h[i][j] > h[i][j - 1]) is_drain = false;
            if (j != m - 1 && h[i][j] > h[i][j + 1]) is_drain = false;

            if (!is_drain) continue;

            ans = max(ans, dfs(i, j));
        }
    }

    printf("%.6lf", ans);
}
```
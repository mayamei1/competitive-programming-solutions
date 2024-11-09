---
tags:
  - competitive-programming/judges/kattis
name: Sheba's Amoebas
date: 2020-04-06
---
#competitive-programming/graph/dfs
## _Solution:_
Iterate through each cell, and check if it is colored in. If it is, increment counter, and DFS to find and mark the connected component as uncolored.

https://open.kattis.com/problems/amoebas
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

int m, n;
vs grid;

void dfs(int i, int j) {
    if (i < 0 || i >= m) return;
    if (j < 0 || j >= n) return;

    if (grid[i][j] == '.') return;
    grid[i][j] = '.';

    dfs(i - 1, j - 1);
    dfs(i, j - 1);
    dfs(i + 1, j - 1);

    dfs(i - 1, j);
    dfs(i, j);
    dfs(i + 1,j);

    dfs(i - 1, j + 1);
    dfs(i, j + 1);
    dfs(i + 1, j + 1);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> m >> n;
    grid = vs(m);
    f (i, 0, m) {
        cin >> grid[i];
    }

    int cnt = 0;
    f (i, 0, m) {
        f (j, 0, n) {
            if (grid[i][j] == '#') {
                cnt++;
                dfs(i, j);
            }
        }
    }
    cout << cnt;
}
```
---
type:
  - competitive-programming
  - kattis
tags:
  - graph/flood-fill
  - ds/disjoint-set
  - graph/bfs
---
#kattis #kattis-island

## _Solution:_
Use flood fill to find and count every island (including the `X`s) and keep track in a disjoint set. Then flood fill to find and count bridges (and maintaining the disjoint set), and for any `X` you come across while flood-filling, you merge that island's set with the bridge's set.

https://open.kattis.com/problems/island
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

using namespace std;

#define LSOne(S) ((S) & -(S))

// Disjoint sets based off index, if a node does not have a parent, then disjoint_set[node] == -1
// create a new disjoint set with vi(n, -1)

// find root (representative of group) of v
int find(vi &disjoint_set, int v) {
    // get root of n
    int root = v;
    while (disjoint_set[root] != -1) {
        root = disjoint_set[root];
    }

    // set every node in branch to have root as parent
    int idx = v;
    while (disjoint_set[idx] != -1) {
        int parent = disjoint_set[idx];
        disjoint_set[idx] = root;
        idx = parent;
    }

    return root;
}

// merge two trees/sets (root is r1)
void merge(vi& disjoint_set, int v, int u) {
    int r1 = find(disjoint_set, v);
    int r2 = find(disjoint_set, u);

    if (r1 != r2) {
        disjoint_set[r2] = r1;
    }
}


vs grid;
vvi visited;
vi root;

void bfs1(int i, int j, int n, int m) {
    queue<ii> q;
    q.push({i, j});
    int r = m * i + j;

    while (!q.empty()) {
        ii c = q.front(); q.pop();
        int ci = c.first, cj = c.second;

        if (ci < 0 || ci >= n) continue;
        if (cj < 0 || cj >= m) continue;
        if (grid[ci][cj] != '#' && grid[ci][cj] != 'X') continue;
        if (visited[ci][cj] == 1) continue;

        visited[ci][cj] = 1;
        merge(root, r, m * ci + cj);
        
        q.push({ci + 1, cj});
        q.push({ci - 1, cj});
        q.push({ci, cj + 1});
        q.push({ci, cj - 1});
    }
}

void bfs2(int i, int j, int n, int m) {
    queue<ii> q;
    q.push({i, j});
    int r = m * i + j;

    while (!q.empty()) {
        ii c = q.front(); q.pop();
        int ci = c.first, cj = c.second;

        if (ci < 0 || ci >= n) continue;
        if (cj < 0 || cj >= m) continue;
        if (visited[ci][cj] == 2) continue;

        if (grid[ci][cj] == 'X') {
            merge(root, r, m * ci + cj);
            continue;
        }

        if (grid[ci][cj] != 'B') continue;

        visited[ci][cj] = 2;
        merge(root, r, m * ci + cj);
        
        q.push({ci + 1, cj});
        q.push({ci - 1, cj});
        q.push({ci, cj + 1});
        q.push({ci, cj - 1});
    }
}

void solve(int t) {
    int is = 0, br = 0, bu = 0;
    int n = grid.size(), m = grid[0].size();
    visited = vvi(n, vi(m, 0));
    root = vi(n * m, -1);

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (visited[i][j] == 1) continue;
            if (grid[i][j] != '#' && grid[i][j] != 'X') continue;

            bfs1(i, j, n, m);
            is++;
        }
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (visited[i][j] == 2) continue;
            if (grid[i][j] != 'B') continue;

            bfs2(i, j, n, m);
            br++;
        }
    }

    unordered_set<int> ans;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (visited[i][j]) ans.insert(find(root, m * i + j));
        }
    }
    bu = ans.size();

    cout << "Map " << t << '\n';
    cout << "islands: " << is << '\n';
    cout << "bridges: " << br << '\n';
    cout << "buses needed: " << bu << '\n';
    cout << '\n';
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t = 1;
    string s;
    while (getline(cin, s)) {
        grid.clear();
        grid.push_back(s);
        while (getline(cin, s) && s != "") {
            grid.push_back(s);
        }

        solve(t++);
    }
}
```
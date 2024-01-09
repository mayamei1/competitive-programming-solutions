---
type:
  - competitive-programming
tags:
  - graph/bfs
  - graph/sssp
---
#kattis #kattis-dungeon

## _Solution:_
BFS through a 3D grid starting from "S".

https://open.kattis.com/problems/dungeon
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

struct i4 {
    int i, j, k, d;
};

int l, r, c;
i4 s;
vector<vs> grid;
vector<vvi> visited;

void solve() {
    queue<i4> q;
    q.push(s);
    while (!q.empty()) {
        i4 cur = q.front(); q.pop();
        if (cur.i < 0 || cur.i >= l) continue;
        if (cur.j < 0 || cur.j >= r) continue;
        if (cur.k < 0 || cur.k >= c) continue;
        if (visited[cur.i][cur.j][cur.k]) continue;
        visited[cur.i][cur.j][cur.k] = 1;
        if (grid[cur.i][cur.j][cur.k] == 'E') {
            cout << "Escaped in " << cur.d << " minute(s).\n";
            return;
        }
        if (grid[cur.i][cur.j][cur.k] == '#') continue;

        q.push({cur.i, cur.j, cur.k + 1, cur.d + 1});
        q.push({cur.i, cur.j, cur.k - 1, cur.d + 1});
        q.push({cur.i, cur.j + 1, cur.k, cur.d + 1});
        q.push({cur.i, cur.j - 1, cur.k, cur.d + 1});
        q.push({cur.i + 1, cur.j, cur.k, cur.d + 1});
        q.push({cur.i - 1, cur.j, cur.k, cur.d + 1});
    }

    cout << "Trapped!\n";
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> l >> r >> c) {
        if (l == 0 && r == 0 && c == 0) break;
        grid = vector<vs>(l, vs(r));
        visited = vector<vvi>(l, vvi(r, vi(c)));

        f (i, 0, l) {
            f (j, 0, r) {
                cin >> grid[i][j];

                f (k, 0, c) {
                    if (grid[i][j][k] == 'S') {
                        s.i = i; s.j = j; s.k = k; s.d = 0;
                    }
                }
            }
        }

        solve();
    }
}
```
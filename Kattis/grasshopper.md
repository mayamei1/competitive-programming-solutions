---
tags:
  - competitive-programming/catalog/kattis
name: Gregory the Grasshopper
---
#competitive-programming/graph/bfs
#competitive-programming/graph/sssp
## _Solution:_
BFS with a chess knight's movement. Print minimum number of hops to reach destination.

https://open.kattis.com/problems/grasshopper
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

struct iii {
    int r;
    int c;
    int d;
};

int r, c, gr, gc, lr, lc;
int solve() {
    queue<iii> q;
    q.push({gr, gc, 0});
    vvi visited(r, vi(c));
    while (!q.empty()) {
        iii cur = q.front(); q.pop();
        if (cur.r < 0 || cur.r >= r) continue;
        if (cur.c < 0 || cur.c >= c) continue;
        if (visited[cur.r][cur.c]) continue;
        visited[cur.r][cur.c] = 1;
        if (cur.r == lr && cur.c == lc) return cur.d;
        q.push({cur.r + 1, cur.c + 2, cur.d + 1});
        q.push({cur.r + 1, cur.c - 2, cur.d + 1});
        q.push({cur.r - 1, cur.c + 2, cur.d + 1});
        q.push({cur.r - 1, cur.c - 2, cur.d + 1});
        q.push({cur.r + 2, cur.c + 1, cur.d + 1});
        q.push({cur.r + 2, cur.c - 1, cur.d + 1});
        q.push({cur.r - 2, cur.c + 1, cur.d + 1});
        q.push({cur.r - 2, cur.c - 1, cur.d + 1});
    }
    return -1;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> r >> c >> gr >> gc >> lr >> lc) {
        gr--; gc--; lr--; lc--;
        int a = solve();
        if (solve() == -1) cout << "impossible\n";
        else cout << a << '\n';
    }    
}
```
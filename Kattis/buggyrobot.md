---
tags:
  - competitive-programming/judges/kattis
name: Buggy Robot
date: 2024-06-23
---
#competitive-programming/graph/dijkstra #competitive-programming/graph/sssp #competitive-programming/graph/weighted #competitive-programming/data-representation #competitive-programming/graph/state-space 
## _Solution:_
Perform Dijkstra's over a graph with the state space of row $i$, column $j$, and instruction $op$. For some $(i,j,op)$, the outgoing edges and their weights are the following. Say we perform the current instruction which results in the robot going to $i_{new},j_{new}$, then there is an edge of weight 0 going to $(i_{new},j_{new},op+1)$. Say we delete the current instruction, then there is an edge of weight 1 going to $(i,j,op+1)$. Say we insert a new instruction that goes to $i_{new},j_{new}$, then there is an edge of weight 1 going to $(i_{new}, j_{new}, op)$. Be sure to account for barriers and the edge of the grid.

https://open.kattis.com/problems/buggyrobot2
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd int
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

int r, c;
vs grid;
const int R = 50 + 2;
int dist[R][R][R];

struct state {
    int i, j, op, d;
};

struct comp {
    bool operator()(const state& a, const state& b) const {
        return a.d > b.d;
    }
};

ii move(state s, char op) {
    int i = s.i, j = s.j;
    int ni = i, nj = j;
    if (op == 'R') nj++;
    if (op == 'L') nj--;
    if (op == 'D') ni++;
    if (op == 'U') ni--;
    if (ni < 0 || ni >= r) return {i, j};
    if (nj < 0 || nj >= c) return {i, j};
    if (grid[ni][nj] == '#') return {i, j};
    return {ni, nj};
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> r >> c;
    grid = vs(r);

    state s = {0, 0, 0, 0}, e;
    for (int i = 0; i < r; i++) {
        cin >> grid[i];
        for (int j = 0; j < c; j++) {
            if (grid[i][j] == 'R') s.i = i, s.j = j;
            if (grid[i][j] == 'E') e.i = i, e.j = j;
        }
    }

    string ops;
    cin >> ops;

    int INF = -1;
    memset(dist, INF, sizeof(dist));

    priority_queue<state, vector<state>, comp> q;
    q.push(s);

    while (!q.empty()) {
        state st = q.top(); q.pop();
        if (st.i < 0 || st.i >= r) continue;
        if (st.j < 0 || st.j >= c) continue;
        if (grid[st.i][st.j] == '#') continue;
        if (dist[st.i][st.j][st.op] != INF) continue;
        if (st.i == e.i && st.j == e.j) {
            cout << st.d << endl;
            return 0;
        }
        dist[st.i][st.j][st.op] = s.d;

        if (st.op != ops.size()) {
            ii m = move(st, ops[st.op]);
            q.push({m.first, m.second, st.op + 1, st.d});
            q.push({st.i, st.j, st.op + 1, st.d + 1});
        }

        q.push({st.i + 1, st.j, st.op, st.d + 1});
        q.push({st.i - 1, st.j, st.op, st.d + 1});
        q.push({st.i, st.j + 1, st.op, st.d + 1});
        q.push({st.i, st.j - 1, st.op, st.d + 1});
    }
}
```
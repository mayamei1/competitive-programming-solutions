---
tags:
  - competitive-programming/judges/kattis
name: Snake
date: 2024-10-07
---
#competitive-programming/complete-search 
## _Solution:_
Observe that if you can revisit points which your tail used to be, then you can guarantee to reach the apple. If the given state is at time $t=0$, then any nodes you visit at $t>0$ can only be revisited at a time greater than revisiting the nodes at $t=0$. If you could never reach a node from $t=0$, then it would also be impossible to revisit any nodes from $t>0$. Thus, we can represent the state of a game by the head, and a grid of boolean values denoting where you have visited. The last observation (which may not be necessary), is that if a solution exists, we can find out within `len(snake)+c` time. If we can revisit where our tail used to be, it can be observed that the worse case scenario would take a constant plus the length of the snake of time in order to reach. If we can't revisit our tail, but an apple can be visited, then the apple is bounded in a small box. Thus, I chose a time step of 20.

With each time step, in a BFS-like fashion, I pop out the tail from original snake if there are any left, and put it in a set of winning positions. Then, I calculate every possible next game states, and check if any of the positions match a winning position.

https://open.kattis.com/problems/snake
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = int;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

vvi delta = {{1, 0, 1}, {-1, 0, 0}, {0, 1, 3}, {0, -1, 2}};

struct state {
    int i, j, dir;
    bitset<100> bs;
};

struct comp_state {
    bool operator()(const state& a, const state& b) const {
        if (a.i != b.i) return a.i < b.i;
        if (a.j != b.j) return a.j < b.j;
        if (a.dir != b.dir) return a.dir < b.dir;
        for (int i = 0; i < 100; i++) {
            if (a.bs[i] != b.bs[i]) return a.bs[i] < b.bs[i];
        }

        return true;
    }
};

int n, m;
vector<string> g;
vii snake;
set<ii> win;

int id(int i, int j) {
    return i * m + j;
}

bool comp(ii a, ii b) {
    return g[a.first][a.second] < g[b.first][b.second];
}

void solve() {
    cin >> n >> m;

    g = vector<string>(n);
    for (auto& s : g) cin >> s;

    bitset<100> st;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (g[i][j] == '.') continue;
            if (g[i][j] == 'A') win.insert({i, j});
            else {
                snake.push_back({i, j});
                st[id(i, j)] = 1;
            }
        }
    }

    sort(snake.begin(), snake.end(), comp);
    set<state, comp_state> q, nq;
    auto [hi, hj] = snake[0];
    state s = {hi, hj, -1, st};
    if (snake.size() > 1) {
        auto [vi, vj] = snake[1];
        for (int i = 0; i < 4; i++) {
            if (vi + delta[i][0] == hi && vj + delta[i][1] == hj) s.dir = delta[i][2];
        }
    }
    q.insert(s);

    for (int t = 0; t < 20; t++) {
        nq.clear();
        if (snake.size()) {
            win.insert(snake.back());
            snake.pop_back();
        }

        for (auto c : q) {
            for (int d = 0; d < 4; d++) {
                int i = c.i + delta[d][0], j = c.j + delta[d][1];
                if (i < 0 || i >= n) continue;
                if (j < 0 || j >= m) continue;
                if (d == c.dir) continue;
                if (win.count({i, j})) {
                    cout << 1 << endl;
                    return;
                }
                if (c.bs[id(i, j)]) continue;
                state next = {i, j, delta[d][2], c.bs};
                next.bs[id(i, j)] = 1;
                nq.insert(next);
            }
        }

        swap(q, nq);
    }

    cout << 0 << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
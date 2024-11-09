---
tags:
  - competitive-programming/judges/atcoder
name: Go Stone Puzzle
date: 2024-07-06
---
#competitive-programming/graph/bfs #competitive-programming/complete-search 
## _Solution:_
Simply try every possible move in a BFS-like manner, and be sure not to revisit the same board states.

https://atcoder.jp/contests/abc361/tasks/abc361_d
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

using namespace std;

void solve() {
    int n;
    cin >> n;
    n += 2;

    string s, t;
    cin >> s >> t;
    s += "..";
    t += "..";

    queue<pair<string, int>> q;
    set<string> vis;
    q.push({s, 0});

    while (q.size()) {
        string c;
        int d;
        tie(c, d) = q.front(); q.pop();

        if (c == t) {
            cout << d << endl;
            return;
        }

        if (vis.count(c)) continue;
        vis.insert(c);

        int i = c.find('.');
        for (int j = 0; j < n - 1; j++) {
            if (c[j] == '.' || c[j + 1] == '.') continue;
            string tmp = c;
            tmp[i] = c[j];
            tmp[i + 1] = c[j + 1];
            tmp[j] = '.';
            tmp[j + 1] = '.';
            q.push({tmp, d + 1});
        }
    }

    cout << -1 << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
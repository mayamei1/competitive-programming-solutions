---
tags:
  - competitive-programming/judges/atcoder
name: Grid Walk
date: 2024-08-02
---
#competitive-programming/trivial #competitive-programming/simulation 
## _Solution:_
Simulate :)

https://atcoder.jp/contests/abc364/tasks/abc364_b
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

void solve() {
    int h, w;
    cin >> h >> w;
    int si, sj;
    cin >> si >> sj;
    si--; sj--;

    vector<string> g(h);
    for (string& s : g) cin >> s;

    string ops;
    cin >> ops;

    for (char op : ops) {
        if (op == 'U') {
            if (si && g[si - 1][sj] == '.') si--;
        } else if (op == 'D') {
            if (si < h - 1 && g[si + 1][sj] == '.') si++;
        } else if (op == 'L') {
            if (sj && g[si][sj - 1] == '.') sj--;
        } else {
            if (sj < w - 1 && g[si][sj + 1] == '.') sj++;
        }
    }

    cout << (si + 1) << ' ' << (sj + 1) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
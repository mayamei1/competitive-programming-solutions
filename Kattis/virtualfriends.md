---
tags:
  - competitive-programming/judges/kattis
name: Virtual Friends
date: 2021-09-14
---
#competitive-programming/ds/disjoint-set 
## _Solution:_
Use disjoint set and keep track of the size of each component.

https://open.kattis.com/problems/virtualfriends
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

vi ds;
vi sz;
int find(int u) {
    int r = u;
    while (ds[r] != -1) r = ds[r];

    int v = u;
    while (v != r) {
        int p = ds[v];
        ds[v] = r;
        v = p;
    }

    return r;
}

int merge(int u, int v) {
    int r1 = find(u), r2 = find(v);
    if (r1 == r2) return sz[r1];
    ds[r2] = r1;
    sz[r1] += sz[r2];
    return sz[r1];
}

void solve() {
    int m;
    cin >> m;

    map<string, int> idx;
    vii edges(m);
    int id = 0;

    for (ii& e : edges) {
        string s, t;
        cin >> s >> t;
        if (idx.count(s) == 0) idx[s] = id++;
        if (idx.count(t) == 0) idx[t] = id++;
        e = {idx[s], idx[t]};
    }

    int n = id;
    ds = vi(n, -1);
    sz = vi(n, 1);
    for (auto [u, v] : edges) {
        cout << merge(u, v) << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
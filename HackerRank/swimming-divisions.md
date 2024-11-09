---
tags:
  - competitive-programming/judges/hackerrank
name: Swimming divisions
date: 2024-10-26
---
#competitive-programming/ds/disjoint-set 
## _Solution:_
Keep track of a disjoint set, as well as the current winner of the division. This can be done with a separate array, or by updating the root of the division accordingly.

https://www.hackerrank.com/contests/lpc-2024/challenges/swimming-divisions
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

// Disjoint sets based off index, if a node does not have a parent, then disjoint_set[node] == -1
// create a new disjoint set with vi(n, -1)

// find root (representative of group) of v
int find(vi &ds, int v) {
    // get root of n
    int root = v;
    while (ds[root] != -1) {
        root = ds[root];
    }

    // set every node in branch to have root as parent
    int idx = v;
    while (ds[idx] != -1) {
        int parent = ds[idx];
        ds[idx] = root;
        idx = parent;
    }

    return root;
}

// merge two trees/sets (root is r1)
void merge(vi& ds, int v, int u) {
    int r1 = find(ds, v);
    int r2 = find(ds, u);

    if (r1 != r2) {
        ds[r2] = r1;
    }
}

void solve() {
    int n;
    cin >> n;

    vector<string> a(n);
    vi ds(n, -1);
    vi top(n);
    for (auto& x : a) cin >> x;

    map<string, int> inv;
    for (int i = 0; i < n; i++) {
        top[i] = i;
        inv[a[i]] = i;
    }

    while (true) {
        string op;
        cin >> op;

        if (op == "END") break;
        if (op == "REQUEST") {
            string s;
            cin >> s;
            int r = find(ds, inv[s]);
            cout << a[top[r]] << endl;
        } else {
            int m;
            cin >> m;
            string s;
            cin >> s;

            int u = inv[s];
            for (int i = 1; i < m; i++) {
                cin >> s;
                merge(ds, u, inv[s]);
            }
            top[find(ds, u)] = u;
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
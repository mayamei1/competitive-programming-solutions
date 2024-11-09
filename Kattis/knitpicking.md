---
tags:
  - competitive-programming/judges/kattis
name: Knitpicking
date: 2022-11-14
---
#competitive-programming/math/combinatorics #competitive-programming/math/pigeon-hole
## _Solution:_
Apply pigeon hole principle. You can handle each type independently. The worst case scenario is $\max(l,r)$ if $a=0$, otherwise it is $\max(l,r,1)$.

https://open.kattis.com/problems/knitpicking
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
    int n;
    cin >> n;

    map<string, int> any;
    map<string, int> left;
    map<string, int> right;
    set<string> vis;
    for (int i = 0; i < n; i++) {
        string type, fit;
        int cnt;
        cin >> type >> fit >> cnt;

        if (fit == "any") any[type] += cnt;
        else if (fit == "left") left[type] += cnt;
        else right[type] += cnt;
        vis.insert(type);
    }

    bool flag = false;
    int ans = 0;
    for (string s : vis) {
        int a = any[s];
        int l = left[s];
        int r = right[s];

        if (a == 0) {
            if (l && r) flag = true;
        } else if (a == 1) {
            if (l || r) flag = true;
        } else flag = true;

        int add = max(l, r);
        add = max(add, min(1, a));
        
        ans += add;
    }

    if (flag) cout << (ans + 1) << endl;
    else cout << "impossible" << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
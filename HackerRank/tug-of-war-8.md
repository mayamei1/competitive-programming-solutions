---
tags:
  - competitive-programming/judges/hackerrank
name: Tug of War
date: 2024-10-28
---
#competitive-programming/complete-search 
## _Solution:_
Try every permutation of $d$.

https://www.hackerrank.com/contests/lpc-2024/challenges/tug-of-war-8
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = double;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

vi d, m;

void solve() {
    int n;
    double p;
    cin >> n >> p;

    d = vi(n), m = vi(n);
    for (double& x : d) cin >> x;
    for (double& x : m) cin >> x;

    vector<int> perm(n);
    iota(perm.begin(), perm.end(), 0);

    int ans = 0;
    do {
        double val = 0;
        for (int i = 0; i < n; i++) {
            val += d[perm[i]] * m[i];
        }
        if (val > p) ans++;
    } while (next_permutation(perm.begin(), perm.end()));
    
    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
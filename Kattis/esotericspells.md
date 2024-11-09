---
tags:
  - competitive-programming/judges/kattis
name: Esoteric Spells
date: 2024-11-05
---
#competitive-programming/greedy 
## _Solution:_
For each bit, get the list of elements with that bit as a 1. Then, iterate from MSB to LSB. If there is a bit with at least one element, we can set that bit to 1. If there are multiple elements, then we can set that bit to 1 (using one element), and set every lower order bits to 1 (using another element).

https://open.kattis.com/problems/esotericspells
```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;
using dd = ll;
using vi = vector<dd>;
using vvi = vector<vi>;
using ii = pair<dd,dd>;
using vii = vector<ii>;
using vvii = vector<vii>;

void solve() {
    int n;
    cin >> n;

    vi a(n);
    for (ll& x : a) cin >> x;

    vvi pos(64);
    for (int i = 0; i < n; i++) {
        for (int j = __lg(a[i]); j >= 0; j--) {
            if ((a[i] >> j) & 1) pos[j].push_back(i);
        }
    }

    int flag = -1;
    vi val(n);
    for (int i = 63; i >= 0; i--) {
        if (flag == -1) {
            if (pos[i].size() == 1) {
                val[pos[i][0]] += 1ll << i;
            } else if (pos[i].size() >= 2) {
                val[pos[i][0]] += 1ll << i;
                flag = pos[i][1];
            }
        } else {
            val[flag] += 1ll << i;
        }
    }

    ll ans = 0;
    for (ll x : val) ans += x;
    cout << ans << endl;
    for (ll x : val) cout << x << ' ';
    cout << endl;
}

int main() {
    int t;
    cin >> t;

    while (t--) solve();
}
```
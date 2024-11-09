---
tags:
  - competitive-programming/judges/kattis
name: Mega Inversions
date: 2024-07-29
---
#competitive-programming/segment-tree 
## _Solution:_
Use one segment/fenwick tree to count the number of inversions by keeping track of numbers to the left of the current element. Then, use another segment/fenwick tree to count the number of "double inversions" by keeping track of inversions for a given number to the left of the current element.

https://open.kattis.com/problems/megainversions
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = ll;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

void add(vi& bit, int i, long delta) {
    for (++i; i < bit.size(); i += (i & (-i))) {
        bit[i] += delta;
    }
}

ll sum(vi& bit, int i) {
    ll val = 0;
    for (++i; i > 0; i -= (i & (-i))) {
        val += bit[i];
    }
    return val;
}

ll sum(vi& bit, int l, int r) {
    return sum(bit, r) - ((l) ? sum(bit, l - 1) : 0ll);
}

void solve() {
    int n;
    cin >> n;

    vi a(n);
    for (ll& aa : a) cin >> aa;

    ll ans = 0;
    vi bit1(n + 2), bit2(n + 2);
    for (int i = 0; i < n; i++) {
        add(bit1, a[i], 1);
        add(bit2, a[i], sum(bit1, a[i] + 1, n));
        ans += sum(bit2, a[i] + 1, n);
    }

    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
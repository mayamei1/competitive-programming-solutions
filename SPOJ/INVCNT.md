---
tags:
  - competitive-programming/judges/spoj
name: Inversion Count
date: 2024-07-29
---
#competitive-programming/segment-tree #competitive-programming/coordinate-compression #competitive-programming/binary-search 
## _Solution:_
We can use a fenwick/segment tree to keep count of numbers to the left of the current element. We can also use coordinate compression so that we limit the size of the fenwick tree to be at most $n$. So for each element, simply query the number of elements that are less than $a_i$.

https://www.spoj.com/problems/INVCNT/
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

// bit(n+1)
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
    for (int& aa : a) cin >> aa;
    vi b = a;
    sort(b.begin(), b.end());
    b.erase(unique(b.begin(), b.end()),  b.end());

    int m = b.size();
    vi bit(m + 1);

    ll ans = 0;
    for (int i = 0; i < n; i++) {
        int j = lower_bound(b.begin(), b.end(), a[i]) - b.begin();
        add(bit, j, 1);
        if (j + 1 == m) continue;
        ans += sum(bit, j + 1, m - 1);
    }

    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
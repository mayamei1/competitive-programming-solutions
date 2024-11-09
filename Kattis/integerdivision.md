---
tags:
  - competitive-programming/judges/kattis
name: Integer Division
date: 2024-09-09
---
#competitive-programming/math/combinatorics
## _Solution:_
Keep track of the frequency of each integer division. Then, for each frequency $f$, sum up $\frac{f\cdot(f-1)}{2}$, or $_fC_2$.

https://open.kattis.com/problems/integerdivision
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
    int n, d;
    cin >> n >> d;

    vi a(n);
    for (int& x : a) cin >> x;

    map<int, int> freq;
    for (int x : a) {
        freq[x / d]++;
    }

    ll ans = 0;
    for (auto [x, f] : freq) {
        ans += 1ll * f * (f - 1) / 2;
    }

    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
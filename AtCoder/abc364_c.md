---
tags:
  - competitive-programming/judges/atcoder
name: Minimum Glutton
date: 2024-08-02
---
#competitive-programming/greedy 
## _Solution:_
Assume worse case for either sweetness or saltiness, then print minimum number of dishes between both.

https://atcoder.jp/contests/abc364/tasks/abc364_c
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
    ll n, x, y;
    cin >> n >> x >> y;

    vi a(n), b(n);
    for (int& t : a) cin >> t;
    for (int& t : b) cin >> t;

    sort(a.begin(), a.end(), greater<>());
    sort(b.begin(), b.end(), greater<>());

    ll asum = 0, bsum = 0;
    for (int i = 0; i < n; i++) {
        if (asum > x || bsum > y) {
            cout << i << endl;
            return;
        }
        asum += a[i];
        bsum += b[i];
    }

    cout << n << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
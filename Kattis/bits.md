---
tags:
  - competitive-programming/judges/kattis
name: Bits
date: 2024-09-16
---
#competitive-programming/trivial #competitive-programming/math 
## _Solution:_
Iterate $n,\lfloor\frac{n}{10}\rfloor,\lfloor\frac{n}{100}\rfloor,\dots$ and count number of one bits, then print maximum count.

https://open.kattis.com/problems/bits
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

    int mx = 0;
    while (n) {
        int t = n;
        int cnt = 0;
        while (t) {
            if (t & 1) cnt++;
            t >>= 1;
        }
        mx = max(mx, cnt);
        n /= 10;
    }

    cout << mx << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
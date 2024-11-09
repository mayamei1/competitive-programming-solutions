---
tags:
  - competitive-programming/judges/codechef
name: Budget Allotment
date: 2024-07-24
---
#competitive-programming/greedy #competitive-programming/sorting 
## _Solution:_
For any element larger than $X$, take away $A_i-X$. Then, for numbers less than $X$, give money to those closest to $X$ first.

https://www.codechef.com/problems/BUDGET25
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
    int n, x;
    cin >> n >> x;

    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];

    sort(a.begin(), a.end(), greater<int>());

    int cnt = 0;
    ll buf = 0;
    for (int i = 0; i < n; i++) {
        if (a[i] >= x) {
            cnt++;
            buf += a[i] - x;
        } else {
            if (x - a[i] > buf) break;
            cnt++;
            buf -= x - a[i];
        }
    }

    cout << cnt << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Older Brother
date: 2024-09-16
---
#competitive-programming/math/number-theory/prime-factors 
## _Solution:_
Check if number of distinct prime factors is exactly 1.

https://open.kattis.com/problems/olderbrother
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

    int p = 2;
    int cnt = 0;
    while (p * p <= n) {
        int flag = 0;
        while (n % p == 0) flag = 1, n /= p;
        cnt += flag;
        p++;
    }

    if (n != 1) cnt++;

    if (cnt == 1) cout << "yes" << endl;
    else cout << "no" << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
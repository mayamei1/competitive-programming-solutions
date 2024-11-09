---
tags:
  - competitive-programming/judges/codechef
name: Equal Pairs (Easy)
date: 2024-09-04
---
#competitive-programming/math #competitive-programming/math/combinatorics #competitive-programming/greedy 
## _Solution:_
Find the maximum frequency of any number (excluding zeros), and add by the number of zeros.

https://www.codechef.com/START150B/problems/MAXEQEASY
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

    vi a(n);
    for (int& x : a) cin >> x;

    int z = 0;
    map<int,int> freq;
    for (int x : a) {
        if (x) freq[x]++;
        else z++;
    }

    ll ans = 0;
    int mx = 0;
    for (auto [x, f] : freq) {
        ans += 1ll * f * (f - 1) / 2;
        mx = max(mx, f);
    }

    ans -= 1ll * mx * (mx - 1) / 2;
    mx += z;
    ans += 1ll * mx * (mx - 1) / 2;
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
---
tags:
  - competitive-programming/judges/atcoder
name: Sum = 0
date: 2024-07-12
---
#competitive-programming/greedy #competitive-programming/math 
## _Solution:_
Via intermediate value theorem, we can guarantee a solution exists if $\sum\limits L_i\le0\le\sum\limits R_i$. We can apply intermediate value theorem, because any integer between $\sum\limits L_i$ and $\sum\limits R_i$ (inclusive) can be made. Say we start by setting all elements to their $L_i$. Then, we must add a total of $-\sum\limits L_i$ to the elements. It doesn't matter which elements we add to, as long as we don't make individual elements greater than their $R_i$.

https://atcoder.jp/contests/abc362/tasks/abc362_c
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd ll
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

using namespace std;

void solve() {
    int n;
    cin >> n;

    vii a(n);
    for (int i = 0; i < n; i++) cin >> a[i].first >> a[i].second;

    ll sum = 0;
    ll buf = 0;
    for (int i = 0; i < n; i++) {
        sum += a[i].first;
        buf += a[i].second - a[i].first;
    }
    if (sum <= 0 && (sum + buf) >= 0) {
        cout << "Yes" << endl;
        ll dif = -sum;
        for (int i = 0; i < n; i++) {
            ll add = min(dif, a[i].second - a[i].first);
            ll ans = a[i].first + add;
            dif -= add;
            cout << ans << ' ';
        }
        cout << endl;
    } else {
        cout << "No" << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
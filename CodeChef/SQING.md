---
tags:
  - competitive-programming/judges/codechef
name: Square String
date: 2024-07-31
---
#competitive-programming/math/combinatorics #competitive-programming/math/modular-arithmetic 
## _Solution:_
For some pair $(i,j)$ where $j<i$, we can count the number of strings where $(i,j)$ is a valid pair. All values to the right of $i$ and all values to the left of $j$ can be either bit. Then, all values between $j+1$ to $i$ must be equal to $i$, while $j$ is negated, thus two possibilities for the values in between $i$ and $j$. This gives us a total contribution of $f(i,j)=2^{j-1}\cdot2^{n-i}\cdot2\cdot(i-j)^2$, or $f(i,j)=2^{n-i+j}\cdot(i-j)^2$. Thus, for some $i$, we can calculate for all $j$: $g(i)=\sum\limits_{j=1}^{i-1}f(i,j)$. Moving things around, we can get $g(i)=2^{n-i}\cdot\sum\limits_{j=1}^{i-1}2^j\cdot(i-j)^2$. We will define $h(i)=\sum\limits_{j=1}^{i-1}2^j\cdot(i-j)^2$. Now, we manipulate $h(i)=(i-1)^2+2\sum\limits_{j=1}^{i-2}2^j\cdot(i-j)^2=(i-1)^2+2h(i-1)$, giving us a recursive definition. Thus, we can iteratively calculate $h(i)$, and accumulate $g(i)$ for all $i$.

https://www.codechef.com/START145B/problems/SQING
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

const int MOD = 1e9 + 7;

ll mod(ll a) {
    return ((a % MOD) + MOD) % MOD;
}

ll bin_pow(ll n, ll k) {
    ll res = 1;
    while (k) {
        if (k & 1) res = mod(res * n);
        n = mod(n * n);
        k >>= 1;
    }
    return res;
}

void solve() {
    ll n;
    cin >> n;

    ll h = 0;
    ll ans = 0;
    for (ll i = 1; i < n; i++) {
        h = mod(mod(2 * h) + mod(i * i));
        ll g = mod(h * bin_pow(2, n - i));
        ans = mod(ans + g);
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
---
tags:
  - competitive-programming/judges/codechef
name: Beautiful Array
date: 2024-07-31
---
#competitive-programming/greedy #competitive-programming/limit-reduction #competitive-programming/data-representation 
## _Solution:_
For some $X$, any one bit is essentially flipping that particular bit. Say we can perform any number of operations. We can look at the position $p$ of the most significant one of $X$, and for any element whose bit at $p$ is 0, we perform an operation on it. Convince yourself that the minimum number of operations needed is equal to the number of continuous segments such that the bit $p$ is 0. If the array of bits at position $p$ is equal to the array of bits at $i$ where $i<p$, then the operations performed for $p$ would also toggle $i$ to 1. However, if any position is all ones, then it would be toggled to 0. So, assuming we have previously calculated all $i$ for a given $p$ as well as the number of operations necessary to toggle $p$ to 1, we can calculate the answer for each query in $O(\log(\max(A)))$ time. Iterate through each one bit of $X$ in descending order. If this bit is all ones (or the number of operations is equal to 0), then we should stop early, since any non-zero number of operations will result in a lower number. If this bit's operation count is at most $K$, then we found where we will toggle to 1. Iterate through all toggled bits for that position, and update the no-operation AND product with the toggled bits.

https://www.codechef.com/problems/ARRBEAUT
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
    int n, q;
    cin >> n >> q;

    vi a(n);
    for (int& aa : a) cin >> aa;

    int base = a[0];
    for (int& aa : a) base &= aa;

    vector<vector<bool>> t(31, vector<bool>(n));
    for (int i = 0; i < 31; i++) {
        for (int j = 0; j < n; j++) t[i][j] = a[j] & (1 << i);
    }

    vi cnt(31);
    vvi flip(31);
    vector<bool> all1(n, 1);
    for (int i = 0; i < 31; i++) {
        int p = (a[0] >> i) & 1;
        for (auto aa : a) {
            int c = (aa >> i) & 1;
            if (c == p) continue;
            if (p == 0) cnt[i]++;
            p = c;
        }
        if (p == 0) cnt[i]++;


        for (int j = 0; j <= i; j++) {
            if (t[i] == t[j] || t[j] == all1) flip[i].push_back(j);
        }
    }

    for (int i = 0; i < q; i++) {
        int k, x;
        cin >> k >> x;

        int ans = base;
        while (x) {
            int j = __lg(x);
            if (cnt[j] == 0) break;
            if (cnt[j] <= k) {
                for (int f : flip[j])
                    if (x & (1 << f)) ans ^= 1 << f;
                break;
            }
            x ^= 1 << j;
        }
        cout << ans << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Martian DNA
date: 2024-10-02
---
#competitive-programming/two-pointers #competitive-programming/ds 
## _Solution:_
Keep track of the indices for each nucleobase. Then, fix the left bound of the substring to be $l=1$. For each nucleobase requirement, find the index of the $q$-th occurrence and store it. If there is not $q$-th occurrence, it is impossible. Keep track of a variable $m$ that keeps track of the maximum among those indices. The minimum length needed for the left bound at $l=1$ is $r=m$. Now, we shift the left bound to $l=2$. This removes the element $a_{1}$, thus we need to update the index of the $q$-th occurrence of $a_1$. This can simply be done by incrementing to the $q+1$-th occurrence. If such occurrence does not exist, then we can stop there. We can keep doing this for all $l$.

https://open.kattis.com/problems/martiandna
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

int n, k, r;

void solve() {
    cin >> n >> k >> r;

    vi a(n);
    vi req(k);
    for (int& x : a) cin >> x;
    for (int i = 0; i < r; i++) {
        int b, q;
        cin >> b >> q;
        req[b] = q;
    }

    vvi idx(k);
    for (int i = 0; i < n; i++) {
        idx[a[i]].push_back(i);
    }

    vi cur(k);
    int mx = 0;
    for (int d = 0; d < k; d++) {
        if (req[d] == 0) continue;
        if (req[d] > idx[d].size()) {
            cout << "impossible" << endl;
            return;
        }
        cur[d] = req[d] - 1;
        mx = max(mx, idx[d][cur[d]]);
    }

    int ans = mx + 1;
    for (int i = 0; i < n; i++) {
        int d = a[i];
        if (req[d] == 0) {
            ans = min(ans, mx - i);
            continue;
        }

        cur[d]++;
        if (cur[d] >= idx[d].size()) break;
        mx = max(mx, idx[d][cur[d]]);
        ans = min(ans, mx - i);
    }

    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
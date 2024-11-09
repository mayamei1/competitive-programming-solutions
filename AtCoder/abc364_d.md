---
tags:
  - competitive-programming/judges/atcoder
name: K-th Nearest
date: 2024-08-02
---
#competitive-programming/binary-search #competitive-programming/sorting 
## _Solution:_
For each query, we can binary search to find the minimum distance away from $b_j$ such that the number of elements in $a$ that is at most $m$ away is at minimum $k$. To calculate the number of elements, assuming $a$ is already sorted, we can binary search to find the two bounds of elements between $b_j-m$ and $b_j+m$.

https://atcoder.jp/contests/abc364/tasks/abc364_d
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
    vii bb(q);
    for (int& t : a) cin >> t;
    sort(a.begin(), a.end());
    for (auto& [b, k] : bb) cin >> b >> k;

    for (auto& [b, k] : bb) {
        int l = -1, h = 2e8;
        while (h - l > 1) {
            int m = (h - l) / 2 + l;
            int ri = upper_bound(a.begin(), a.end(), b + m) - a.begin() - 1;
            int li = lower_bound(a.begin(), a.end(), b - m) - a.begin();
            if ((ri - li + 1) >= k) h = m;
            else l = m;
        }
        cout << h << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
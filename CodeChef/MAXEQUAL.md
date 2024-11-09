---
tags:
  - competitive-programming/judges/codechef
name: Equal Pairs (Hard)
date: 2024-09-04
---
#competitive-programming/ds #competitive-programming/math/combinatorics 
## _Solution:_
You can keep track of the count of each equal pairs without doing zero operations. Say we are performing some event and we have $f_y$ counts of $y$ before the event. Then, we can increment $f_y$ to a sum $s$ to update the count of equal pairs. To handle doing the zero operations, we will first update $f_y:=f_y+1$, then update the max frequency of any $f$, denoted $f_m$. The answer requires taking out the count of equal pairs of $m$ and adding back count of pairs after turning all zeros to $m$, or $s-\frac{f_{m}\cdot(f_{m}-1)}{2}+\frac{(f_{m}+z)(f_{m}+z-1)}{2}$.

https://www.codechef.com/START150B/problems/MAXEQUAL
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

    int z = n;
    ll base = 0;
    int mx = 0;
    map<int, int> freq;
    for (int i = 0; i < n; i++) {
        int x, y;
        cin >> x >> y;
        z--;
        base += freq[y];
        freq[y]++;
        mx = max(mx, freq[y]);

        ll ans = base;
        ans -= 1ll * mx * (mx - 1) / 2;
        ans += 1ll * (mx + z) * (mx + z - 1) / 2;
        cout << ans << ' ';
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
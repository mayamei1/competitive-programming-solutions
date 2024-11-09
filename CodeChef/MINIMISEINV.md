---
tags:
  - competitive-programming/judges/codechef
name: Minimise Inversions
date: 2024-07-24
---
#competitive-programming/greedy 
## _Solution:_
If we had to choose $x$ 1's to flip and $y$ 0's to flip, we would want to flip the left most 1's and the right most 0's, and any flipped 1's must be before flipped 0's. This leaves us with $K$ different possibilities for $x$ and $y$.

https://www.codechef.com/problems/MINIMISEINV
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
    int n, k;
    cin >> n >> k;

    string s;
    cin >> s;

    int ans = 1e9;

    for (int l = 0; l <= k; l++) {
        int r = k - l;

        string t = s;
        int a = l;
        int i = 0;
        int last = -1;
        while (a--) {
            while (i < n && t[i] != '1') i++;
            if (i == n) break;
            t[i] = '0';
            last = i;
        }

        a = r;
        int j = n - 1;
        while (a--) {
            while (j > last && t[j] != '0') j--;
            if (j == -1) break;
            t[j] = '1';
        }

        int ones = 0;
        int inv = 0;
        for (int i = 0; i < n; i++) {
            if (t[i] == '1') ones++;
            else inv += ones;
        }

        ans = min(ans, inv);
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
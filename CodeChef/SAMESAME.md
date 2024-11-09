---
tags:
  - competitive-programming/judges/codechef
name: Nearly Equal
date: 2024-07-03
---
#competitive-programming/complete-search #competitive-programming/string 
## _Solution:_
Iterate through every possible start of the contiguous substring of $B$, then do a linear check of the Hamming distance.

https://www.codechef.com/START141D/problems/SAMESAME
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd int
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

using namespace std;

void solve() {
    int n, m;
    cin >> n >> m;

    string a, b;
    cin >> a >> b;

    int ans = 100000;
    for (int i = 0; i <= (n - m); i++) {
        int val = 0;
        for (int j = 0; j < m; j++) {
            val += a[i+j] != b[j];
        }
        ans = min(ans, val);
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
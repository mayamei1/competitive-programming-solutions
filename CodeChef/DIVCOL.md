---
tags:
  - competitive-programming/judges/codechef
name: Non-Divisor Array
date: 2024-07-17
---
#competitive-programming/greedy #competitive-programming/limit-reduction 
## _Solution:_
We can set $A_1=1$, then for each $A_i$, find the maximum of value of all divisors, and set $A_i$ to that value, plus 1.


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
    int n;
    cin >> n;

    vi a(n + 1);
    a[1] = 1;
    int c = 1;
    for (int i = 2; i <= n; i++) {
        int mx = 0;
        for (int j = 1; j * j <= i; j++) {
            if (i % j) continue;
            mx = max(mx, a[j]);
            mx = max(mx, a[i / j]);
        }
        a[i] = mx + 1;
        c = max(c, mx + 1);
    }

    cout << c << endl;
    for (int i = 1; i <= n; i++) {
        cout << a[i] << ' ';
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
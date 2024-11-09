---
tags:
  - competitive-programming/judges/atcoder
name: Make Them Narrow
date: 2024-07-06
---
#competitive-programming/two-pointers #competitive-programming/sorting #competitive-programming/greedy 
## _Solution:_
Observe that you would always want to remove the extrema to get the minimum. If you have a sorted $A$, then you can use a two pointer-like solution where the range denotes which elements are left.

https://atcoder.jp/contests/abc361/tasks/abc361_c
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

const int N = 2e5 + 2;
int a[N];

void solve() {
    int n, k;
    cin >> n >> k;

    for (int i = 0; i < n; i++) cin >> a[i];

    sort(a, a + n);

    int ans = 1e9 + 5;
    for (int i = 0; i < n; i++) {
        int j = n - (k - i) - 1;
        if (j < n) {
            ans = min(ans, a[j] - a[i]);
        }
    }
    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
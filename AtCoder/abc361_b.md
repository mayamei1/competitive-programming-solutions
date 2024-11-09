---
tags:
  - competitive-programming/judges/atcoder
name: Intersection of Cuboids
date: 2024-07-06
---
#competitive-programming/geometry 
## _Solution:_
Check that the following are all positive: $\min(d, j)-\max(a,g)$, $\min(e,k)-\max(b,h)$, and $\min(f,l)-\max(c,i)$.

https://atcoder.jp/contests/abc361/tasks/abc361_b
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
    int a, b, c, d, e, f;
    int g, h, i, j, k, l;
    cin >> a >> b >> c >> d >> e >> f;
    cin >> g >> h >> i >> j >> k >> l;

    int ff = max(min(d, j) - max(a, g), 0);
    int ss = max(min(e, k) - max(b, h), 0);
    int tt = max(min(f, l) - max(c, i), 0);

    if (ff && ss && tt) cout << "Yes" << endl;
    else cout << "No" << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
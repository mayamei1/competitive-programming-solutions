---
tags:
  - competitive-programming/judges/codechef
name: Redundant Array
date: 2024-07-03
---
#competitive-programming/math #competitive-programming/greedy 
## _Solution:_
Observe that since the cost of the operation is simply the length times $x$, it will be no different to split up a single operation to single element operations. Thus, we can keep track of the count of each element, then iterate through each distinct element $x$ with frequency $f$, and find the minimum $x\cdot(n-f)$.

https://www.codechef.com/START141D/problems/REDUARRAY
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

    map<int, int> f;
    for (int i = 0; i < n; i++) {
        int a;
        cin >> a;
        f[a]++;
    }

    ll ans = n;
    for (auto [a, cnt] : f) {
        ans = min(ans, (1ll * a) * (n - cnt));
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
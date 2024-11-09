---
tags:
  - competitive-programming/judges/hackerrank
name: Fastest Relay Team
date: 2024-10-26
---
#competitive-programming/math/pigeon-hole #competitive-programming/complete-search 
## _Solution:_
It's easy to see that we only need to check the top 4 fastest swimmers of any stroke. Then, we can try every valid combination of those swimmers.

https://www.hackerrank.com/contests/lpc-2024/challenges/fastest-relay-team
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

vvii a;
set<int> path;
int dfs(int j) {
    if (j == 4) return 0;

    int mn = 1e9;
    for (int i = 0; i < 4; i++) {
        if (path.count(a[j][i].second)) continue;
        path.insert(a[j][i].second);
        mn = min(mn, a[j][i].first + dfs(j + 1));
        path.erase(a[j][i].second);
    }

    return mn;
}

void solve() {
    int n;
    cin >> n;
    a = vvii(4, vii(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < 4; j++) {
            cin >> a[j][i].first;
            a[j][i].second = i;
        }
    }

    for (int j = 0; j < 4; j++) {
        sort(a[j].begin(), a[j].end());
    }

    cout << dfs(0) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
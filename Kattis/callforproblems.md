---
tags:
  - competitive-programming/judges/kattis
name: Call for Problems
date: 2024-10-05
---
#competitive-programming/trivial 
## _Solution:_
Count number of odd numbers.

https://open.kattis.com/problems/callforproblems
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

    int ans = 0;
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;

        if (x % 2) ans++;
    }

    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
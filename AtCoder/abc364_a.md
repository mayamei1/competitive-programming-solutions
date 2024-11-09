---
tags:
  - competitive-programming/judges/atcoder
name: Glutton Takahashi
date: 2024-08-02
---
#competitive-programming/trivial 
## _Solution:_
Check all but the last consecutive pair to see if both are sweet.

https://atcoder.jp/contests/abc364/tasks/abc364_a
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

    vector<string> s(n);
    for (string& ss : s) cin >> ss;

    for (int i = 1; i < n - 1; i++) {
        if (s[i] == "sweet" && s[i] == s[i - 1]) {
            cout << "No" << endl;
            return;
        }
    }

    cout << "Yes" << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
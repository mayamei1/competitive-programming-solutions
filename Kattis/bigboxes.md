---
tags:
  - competitive-programming/judges/kattis
name: Big Boxes
date: 2024-09-30
---
#competitive-programming/binary-search 
## _Solution:_
Binary search the maximum total weight before switching to a new group. If the number of groups is less than or equal to the maximum amount of groups, then we can search smaller.

https://open.kattis.com/problems/bigboxes
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

    vi a(n);
    for (int& x : a) cin >> x;

    int l = *max_element(a.begin(), a.end()) - 1, h = 1e9;
    while (h - l > 1) {
        int m = (h - l) / 2 + l;

        int groups = 1;
        int sum = 0;
        for (int x : a) {
            if (sum + x > m) {
                groups++;
                sum = 0;
            }
            sum += x;
        }

        if (groups <= k) h = m;
        else l = m;
    }

    cout << h << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
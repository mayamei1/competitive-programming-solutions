---
tags:
  - competitive-programming/judges/codechef
name: Find Multiset State
date: 2024-09-04
---
#competitive-programming/math 
## _Solution:_
Print $a_{k+1},a_{k+2},a_{k+3},\dots,a_{n-1}$. Then print the sum of $a_{n}+a_{1}+a_{2}+a_{3}+\cdots+a_{k}$.

https://www.codechef.com/START150B/problems/ARRAYSTATE
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

    for (int i = k; i < n - 1; i++) cout << a[i] << ' ';
    int sum = a[n - 1];
    for (int i = 0; i < k; i++) sum += a[i];
    cout << sum << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
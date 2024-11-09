---
tags:
  - competitive-programming/judges/kattis
name: From A to B
date: 2024-09-16
---
#competitive-programming/greedy #competitive-programming/math 
## _Solution:_
While $a>b$, we must divide by 2. Once $a\le b$, add by 1 $b-a$ times. This is optimal, since if you perform the plus 1 operations first, it require more operations.

https://open.kattis.com/problems/fromatob
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
    int a, b;
    cin >> a >> b;

    int cnt = 0;
    while (a > b) {
        if (a % 2) a++, cnt++;
        a /= 2;
        cnt++;
    }
    cnt += b - a;
    cout << cnt << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
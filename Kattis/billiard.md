---
tags:
  - competitive-programming/judges/kattis
name: Billiard
date: 2024-10-29
---
#competitive-programming/geometry 
## _Solution:_
The distance in the $x$ direction is simply $a\cdot m$, while $y$ is $b\cdot n$. With this, we can calculate the angle, and with $s$, we can calculate the speed.

https://open.kattis.com/problems/billiard
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

bool solve() {
    int a, b, s, m, n;
    cin >> a >> b >> s >> m >> n;
    if (!(a || b || s || m || n)) return false;

    int x = a * m, y = b * n;
    double angle = atan2(y, x) * 180 / atan2(0, -1);
    double dist = sqrt((double)x * x + (double)y * y);

    printf("%.2lf %.2lf\n", angle, dist / s);
    return true;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (solve());
}
```
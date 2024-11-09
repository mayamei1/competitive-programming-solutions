---
tags:
  - competitive-programming/judges/kattis
name: Bikes and Barricades
date: 2024-10-05
---
#competitive-programming/geometry 
## _Solution:_
For each barricade, check if it goes through the y-axis, then calculate the point where it intersects. If the y value is negative, discard it, otherwise, keep track of the minimum of such value.

https://open.kattis.com/problems/bikesandbarricades
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

    double ans = -1.0;
    for (int i = 0; i < n; i++) {
        double x1, y1, x2, y2;
        cin >> x1 >> y1 >> x2 >> y2;

        if (x1 >= x2) {
            swap(x1, x2);
            swap(y1, y2);
        }

        if (x1 <= 0 && 0 <= x2) {
            double y = y1 + (y2 - y1) * (0 - x1) / (x2 - x1);
            if (y < 0) continue;
            if (ans < 0) ans = y;
            else ans = min(ans, y);
        }
    }

    printf("%.9lf", ans);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
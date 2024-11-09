---
tags:
  - competitive-programming/judges/kattis
name: Ellipse Eclipse
date: 2024-10-06
---
#competitive-programming/binary-search #competitive-programming/geometry
## _Solution:_
Note that every point in an ellipse can be determined as the sum of distances from the foci being equal to the major axis. Then, it is easy to see that the left bound must be less than the left most focal point. If we binary search the left bound, we have a fixed $x$. It can be observed for a fixed $x$ that the formula of sum of distances from foci is convex if you vary $y$. Thus, we can ternary search for the minimum sum of distances. If the sum of distances is less than or equal to the major axis, we are inside of the ellipse, and otherwise we are outside. Do this for all directions (which can be achieved by doing some reflecting).

https://open.kattis.com/problems/ellipseeclipse
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

double dist(double x, double y) {
    return sqrt(x * x + y * y);
}

double dist2(double x, double y, double x1, double y1, double x2, double y2) {
    return dist(x - x1, y - y1) + dist(x - x2, y - y2);
}

double ts(double x, double x1, double y1, double x2, double y2) {
    double l = -2000, h = 2000;
    while (h - l > 1e-9) {
        double m1 = (h - l) / 3.0 + l;
        double m2 = (h - l) * 2.0 / 3.0 + l;
        double a1 = dist2(x, m1, x1, y1, x2, y2);
        double a2 = dist2(x, m2, x1, y1, x2, y2);

        if (a1 < a2) h = m2;
        else l = m1;
    }

    return dist2(x, l, x1, y1, x2, y2);
}

double bs(double x1, double y1, double x2, double y2, double a) {
    double l = -2000, h = x1;
    while (h - l > 1e-9) {
        double m = (h - l) / 2.0 + l;
        
        double mn = ts(m, x1, y1, x2, y2);
        if (mn >= a) l = m;
        else h = m;
    }

    return l;
}

void solve() {
    double x1, y1, x2, y2, a;
    cin >> x1 >> y1 >> x2 >> y2 >> a;

    if (x1 > x2) {
        swap(x1, x2);
        swap(y1, y2);
    }

    double xl = bs(x1, y1, x2, y2, a);
    double xh = -bs(-x2, y2, -x1, y1, a);
    
    if (y1 > y2) {
        swap(x1, x2);
        swap(y1, y2);
    }

    double yl = bs(y1, x1, y2, x2, a);
    double yh = -bs(-y2, x2, -y1, x1, a);

    printf("%.9lf %.9lf %.9lf %.9lf\n", xl, yl, xh, yh);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
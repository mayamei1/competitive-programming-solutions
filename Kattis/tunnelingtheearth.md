---
tags:
  - competitive-programming/judges/kattis
name: Tunnelling the Earth
date: 2024-10-29
---
#competitive-programming/geometry 
## _Solution:_
Use the angles to calculate the coordinates, then calculate the tunnel distance. Then, calculate the angle between the two coordinates from the center, and calculate the line segment of the circumference.

https://open.kattis.com/problems/tunnelingtheearth
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = double;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

double r = 6371009;

vi convert(double theta, double rho) {
    theta *= atan2(0, -1) / 180;
    rho *= atan2(0, -1) / 180;
    double x = r * cos(theta) * cos(rho);
    double y = r * sin(theta) * cos(rho);
    double z = r * sin(rho);
    return {x, y, z};
}

vi sub(vi a, vi b) {
    double x = a[0] - b[0];
    double y = a[1] - b[1];
    double z = a[2] - b[2];
    return {x, y, z};
}

double dist(vi a) {
    double x = a[0], y = a[1], z = a[2];
    return sqrt(x * x + y * y + z * z);
}

double dot(vi a, vi b) {
    double x = a[0] * b[0];
    double y = a[1] * b[1];
    double z = a[2] * b[2];
    return x + y + z;
}

void solve() {
    double lat, lon;
    cin >> lat >> lon;
    vi p1 = convert(lon, lat);
    cin >> lat >> lon;
    vi p2 = convert(lon, lat);
    double d1 = dist(sub(p1, p2));
    double angle = acos(dot(p1, p2) / dist(p1) / dist(p2));
    double d2 = angle * r;

    printf("%lf\n", fabs(d1 - d2));
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
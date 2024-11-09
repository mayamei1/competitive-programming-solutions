---
tags:
  - competitive-programming/judges/kattis
name: Robot Protection
date: 2024-10-29
---
#competitive-programming/geometry/convex-hull #competitive-programming/geometry/polygon-area 
## _Solution:_
Find convex hull and calculate the area of the hull.

https://open.kattis.com/problems/robotprotection
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

// set the data type by changing the define of dd
ii p0;
bool collinear = false;

int orient(ii a, ii b, ii c) {
    dd v = a.first*(b.second-c.second)+b.first*(c.second-a.second)+c.first*(a.second-b.second);
    if (v < 0) return -1; if (v > 0) return 1;
    return 0;
}

bool cw(ii a, ii b, ii c) {
    int o = orient(a, b, c);
    return o < 0 || (collinear && o == 0);
}

bool comp1(ii a, ii b) {
    if (a.second == b.second) return a.first < b.first;
    return a.second < b.second;
}

bool comp2(ii a, ii b) {
    int o = orient(p0, a, b);
    dd dax = p0.first-a.first, day = p0.second-a.second, dbx = p0.first-b.first, dby = p0.second-b.second;
    if (o == 0)
        return dax*dax+day*day < dbx*dbx+dby*dby;
    return o < 0;
}

double area(vii& a) {
    double res = 0;
    for (int i = 0; i < a.size(); i++) {
        ii p = i ? a[i - 1] : a.back();
        ii q = a[i];
        res += (p.first - q.first) * (p.second + q.second);
    }
    return fabs(res) / 2;
}

bool solve() {
    int n;
    cin >> n;

    if (n == 0) return false;

    vii a(n);
    for (ii& x : a) cin >> x.first >> x.second;
    p0 = *min_element(a.begin(), a.end(), comp1);
    sort(a.begin(), a.end(), comp2);

    if (collinear) {
        int i = a.size() - 1;
        while (i >= 0 && orient(p0, a[i], a.back()) == 0) i--;
        reverse(a.begin()+i+1, a.end());
    }

    vii st;
    for (int i = 0; i < n; i++) {
        while (st.size() > 1 && !cw(st[st.size() - 2], st.back(), a[i]))
            st.pop_back();
        st.push_back(a[i]);
    }

    if (!collinear && st.size() == 2 && st[0] == st[1])
        st.pop_back();

    printf("%.1lf\n", area(st));
    return true;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (solve());
}
```
---
tags:
  - "#competitive-programming/judges/atcoder"
name: Right Triangle
date:
---
#competitive-programming/geometry 
## _Solution:_
Right angles can be found by picking a center point, then creating vectors pointing at the other two points. If the dot product of the two vectors is 0, then it is a right angle.

https://atcoder.jp/contests/abc362/tasks/abc362_b
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd int
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

using namespace std;

void solve() {
    vii p(3);
    for (int i = 0; i < 3; i++) cin >> p[i].first >> p[i].second;

    for (int i = 0; i < 3; i++) {
        ii a = p[i];
        ii b = p[(i + 1) % 3];
        ii c = p[(i + 2) % 3];

        ii ab = {b.first - a.first, b.second - a.second};
        ii ac = {c.first - a.first, c.second - a.second};

        int dot = ab.first * ac.first + ab.second * ac.second;
        if (dot == 0) {
            cout << "Yes" << endl;
            return;
        }
    }

    cout << "No" << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Convex Hull
date: 2024-05-14
---
#competitive-programming/geometry/convex-hull
## _Solution:_
Print convex hull without collinear edges in counter clockwise direction.

https://open.kattis.com/problems/convexhull
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd ll
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;

    while (cin >> n && n) {
        vii a(n);
        for (int i = 0; i < n; i++) {
            cin >> a[i].first >> a[i].second;
        }

        p0 = *min_element(a.begin(), a.end());
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

        reverse(st.begin(), st.end());
        cout << st.size() << '\n';
        for (ii s : st) {
            cout << s.first << ' ' << s.second << '\n';
        }
    }
}
```
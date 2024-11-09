---
tags:
  - competitive-programming/judges/kattis
name: Enclosure
date: 2024-05-14
---
#competitive-programming/geometry/convex-hull #competitive-programming/geometry/polygon-area #competitive-programming/binary-search #competitive-programming/ds/range-query/running-sum 
## _Solution:_
Start with finding the convex hull of the points you have control over, then find the area. Keep track of a running sum of the area (as you will need to add/subtract out different edges). For each point you don't have control over (search point), find where the point would fit in the convex hull's Graham scan, then check if it is in or out of the convex hull via a CW/CCW check with the two neighboring points. Then, you will need to do two (cyclic) binary searches to find the bounds of the edges that are discarded if the search point was added in. The first bound of the binary searches is the neighboring point, and the second bound is $P_0$ (the bottom most, then left most point). The only time this could fail is if the search point's $y$ is less than $P_0$'s $y$, thus you should instead use the top-then-right most point. You can tell if edge $(p,q)$ needs to be discarded if $(p,s)$ to $(s, q)$ is clockwise, where $s$ is the search point.

https://open.kattis.com/problems/enclosure
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

ii p0, p1;
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

bool comp1(const ii a, const ii b) {
    if (a.second == b.second) return a.first < b.first;
    return a.second < b.second;
}

bool comp2(const ii a, const ii b) {
    int o = orient(p0, a, b);
    dd dax = p0.first-a.first, day = p0.second-a.second, dbx = p0.first-b.first, dby = p0.second-b.second;
    if (o == 0)
        return dax*dax+day*day < dbx*dbx+dby*dby;
    return o < 0;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, k;
    cin >> n >> k;

    vii a(k), b(n - k);
    for (int i = 0; i < k; i++) {
        cin >> a[i].first >> a[i].second;
    }
    for (int i = 0; i < (n - k); i++) {
        cin >> b[i].first >> b[i].second;
    }

    p0 = *min_element(a.begin(), a.end(), comp1);
    p1 = *max_element(a.begin(), a.end(), comp1);
    sort(a.begin(), a.end(), comp2);

    if (collinear) {
        int i = a.size() - 1;
        while (i >= 0 && orient(p0, a[i], a.back()) == 0) i--;
        reverse(a.begin()+i+1, a.end());
    }

    vii st;
    for (int i = 0; i < k; i++) {
        while (st.size() > 1 && !cw(st[st.size() - 2], st.back(), a[i]))
            st.pop_back();
        st.push_back(a[i]);
    }

    if (!collinear && st.size() == 2 && st[0] == st[1])
        st.pop_back();
    int m = st.size();

    ll base = 0;
    vi r_area(m);
    int p0_i, p1_i;
    for (int i = 0; i < m; i++) {
        ii p = i ? st[i - 1] : a.back();
        ii q = st[i];
        base += (p.first - q.first) * (p.second + q.second);
        r_area[i] = base;

        if (st[i] == p0) p0_i = i;
        if (st[i] == p1) p1_i = i;
    }

    ll max_area = abs(base);
    for (int i = 0; i < (n - k); i++) {
        int itr = lower_bound(st.begin(), st.end(), b[i], comp2) - st.begin();
        int h_p = itr, l_p = itr ? itr - 1 : m - 1;
        int l, h;
        
        // search high point
        l = h_p;
        if (b[i].second < p0.second) h = p1_i;
        else h = p0_i + m;
        
        while (l <= h) {
            int m_p = l + (h - l) / 2;
            int p_p = m_p - 1;

            if (cw(st[(p_p + m) % m], b[i], st[(m_p + m) % m])) {
                h_p = max(h_p, m_p + m);
                l = m_p + 1;
            } else {
                h = m_p - 1;
            }
        }

        // search low point
        if (b[i].second < p0.second) l = p1_i;
        else l = p0_i;
        if (l_p < l) l_p += m;
        h = l_p;

        while (l <= h) {
            int m_p = l + (h - l) / 2;
            int n_p = m_p + 1;

            if (cw(st[m_p % m], b[i], st[n_p % m])) {
                l_p = min(l_p, m_p);
                h = m_p - 1;
            } else {
                l = m_p + 1;
            }
        }

        l_p %= m;
        h_p %= m;

        ll n_area;
        if (h_p < l_p) {
            n_area = r_area[l_p] - r_area[h_p];
        } else {
            n_area = base - r_area[h_p] + r_area[l_p];
        }
        ii p = st[l_p];
        ii t = b[i];
        ii q = st[h_p];
        n_area += (p.first - t.first) * (p.second + t.second);
        n_area += (t.first - q.first) * (t.second + q.second);

        n_area = abs(n_area);
        max_area = max(max_area, n_area);
    }
    cout << (max_area / 2) << '.' << ((max_area % 2) * 5);
}
```
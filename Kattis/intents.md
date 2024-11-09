---
tags:
  - competitive-programming/judges/kattis
name: 
date: 2024-06-22
---
#competitive-programming/geometry #competitive-programming/greedy #competitive-programming/sorting 
## _Solution:_
The volume under a triangle is simply the area of the shadow multiplied by the average of the heights, or $V=A\frac{h_{1}+h_{2}+h_{3}}{3}$. Thus, if we were to add up all of the volumes, we would get
$$
V=A_{1,2}\frac{h_{1}+h_{2}+h_{0}}{3}+A_{2,3}\frac{h_{2}+h_{3}+h_{0}}{3}+\cdots+A_{n,1}\frac{h_{n}+h_{1}+h_{0}}{3}
$$
, where $A_{i,j}$ indicates the area of of the points $i$, $j$, and the origin, and $h_0$ is the height at the origin. Moving some values around, we can get
$$
3V=h_1(A_{n,1}+A_{1,2})+h_2(A_{1,2}+A_{2,3})+\cdots+h_n(A_{n-1,n}+A_{n,1})+h_0(A_{1,2}+A_{2,3}+\cdots+A_{n,1})
$$
Thus, it is optimal to assign the largest pole to the origin. For the rest of the poles, you want to assign the largest poles with the location $i$ such that $A_{i-1,i}+A_{i,i+1}$ is largest.

https://open.kattis.com/problems/intents
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

bool comp(ii a, ii b) {
    return atan2(a.second, a.first) < atan2(b.second, b.first);
}

ll cross(ii a, ii b) {
    return abs(a.first * b.second - a.second * b.first);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;
    n--;

    vii p(n);
    for (int i = 0; i < n; i++) {
        cin >> p[i].first >> p[i].second;
    }

    vi h(n + 1);
    for (int i = 0; i <= n; i++) {
        cin >> h[i];
    }

    sort(p.begin(), p.end(), comp);    
    sort(h.begin(), h.end(), greater<int>());

    ll h0 = h[0];

    ll ans = 0;
    vi base(n);
    ll a = cross(p[n - 1], p[0]);
    ans += a * h0;
    base[0] += a;
    base[n - 1] += a;
    for (int i = 1; i < n; i++) {
        a = cross(p[i - 1], p[i]);
        ans += a * h0;
        base[i - 1] += a;
        base[i] += a;
    }

    sort(base.begin(), base.end(), greater<int>());

    for (int i = 0; i < n; i++) {
        ans += base[i] * h[i + 1];
    }

    printf("%.6lf", ans / 6.0);
}
```
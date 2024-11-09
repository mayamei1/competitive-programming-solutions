---
tags:
  - competitive-programming/judges/kattis
name: Brownie Points I
date: 2019-03-20
---
#competitive-programming/trivial 
## _Solution:_
Centered around point $p_{\lfloor N/2\rfloor}$, count the points that are strictly in Q1 and Q3, and for Q2 and Q4.

https://open.kattis.com/problems/browniepoints
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

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    while (cin >> n && n != 0) {
        vii p(n);
        for (int i = 0; i < n; i++) {
            cin >> p[i].first >> p[i].second;
        }

        ii m = p[n / 2];
        int a = 0, b = 0;
        for (ii c : p) {
            int x = c.first - m.first, y = c.second - m.second;
            if (x > 0 && y > 0) a++;
            if (x < 0 && y < 0) a++;
            if (x > 0 && y < 0) b++;
            if (x < 0 && y > 0) b++;
        }

        cout << a << ' ' << b << endl;
    }
}
```
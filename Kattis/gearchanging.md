---
tags:
  - competitive-programming/judges/kattis
name: Gear Changing
date: 2024-06-24
---
#competitive-programming/complete-search 
## _Solution:_
Iterate through each combination of gears and get $\frac{d_{j}}{c_{i}}$. Sort $\frac{d_{j}}{c_{i}}$ and check that they are within $P\%$ of each other.

https://open.kattis.com/problems/gearchanging
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

const int N = 100 + 2;
int c[N];
int d[N];

bool comp(ii& a, ii& b) {
    return a.first * b.second < b.first * a.second;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m, p;
    cin >> n >> m >> p;

    for (int i = 0; i < n; i++) {
        cin >> c[i];
    }

    for (int i = 0; i < m; i++) {
        cin >> d[i];
    }

    vii vals;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            vals.push_back({d[j], c[i]});
        }
    }

    sort(vals.begin(), vals.end(), comp);

    for (int i = 1; i < vals.size(); i++) {
        ii a = vals[i - 1];
        ii b = vals[i];

        if (a.first * b.second * (100 + p) < b.first * a.second * 100) {
            cout << "Time to change gears!" << endl;
            return 0;
        }
    }

    cout << "Ride on!" << endl;
}
```
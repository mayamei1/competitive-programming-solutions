---
tags:
  - competitive-programming/judges/kattis
name: A Different Problem
date: 2019-03-20
---
#competitive-programming/trivial 
## _Solution:_
Get absolute difference of two integers. Make sure to use 64-bit integers.

https://open.kattis.com/problems/different
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

    ll a, b;
    while (cin >> a >> b) {
        cout << (abs(a - b)) << endl;
    }
}
```
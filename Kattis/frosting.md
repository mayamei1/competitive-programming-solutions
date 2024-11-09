---
tags:
  - competitive-programming/judges/kattis
name: Frosting on the Cake
date: 2024-04-03
---
#competitive-programming/math #competitive-programming/limit-reduction #competitive-programming/geometry 
## _Solution:_
Save $A$ and $B$ as the sums with $\mod3$ parity. Each color can be found by doing sum of products of different $A$ and $B$ parities. Also be weary that $(i,j)$ are $1$-indexed.

https://open.kattis.com/problems/frosting
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <list>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>
#include <bitset>
#include <iomanip>

#define ll long long int
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    ll n;
    cin >> n;

    vi a(3), b(3);
    f (i, 0, n) {
        ll v;
        cin >> v;
        a[i % 3] += v;
    }
    f (i, 0, n) {
        ll v;
        cin >> v;
        b[i % 3] += v;
    }

    if (n % 3 == 0) {
        ll sb = b[0] + b[1] + b[2];
        cout << (a[1]*sb) << ' ' << (a[2]*sb) << ' ' << (a[0]*sb) << endl;
    } else if (n % 3 == 1) {
        ll x = a[2]*b[2] + a[0]*b[1] + a[1]*b[0];
        ll y = a[1]*b[1] + a[0]*b[2] + a[2]*b[0];
        ll z = a[0]*b[0] + a[1]*b[2] + a[2]*b[1];
        cout << x << ' ' << y << ' ' << z << endl;
    } else {
        ll x = a[0]*b[2] + a[1]*b[0] + a[2]*b[1];
        ll y = a[0]*b[1] + a[1]*b[2] + a[2]*b[0];
        ll z = a[0]*b[0] + a[1]*b[1] + a[2]*b[2];
        cout << x << ' ' << y << ' ' << z << endl;
    }
}
```
---
tags:
  - competitive-programming/catalog/kattis
name: Noonerized Spumbers
---
#competitive-programming/complete-search
## _Solution:_
Search every possible pairs of prefixes for each pair of numbers -- $(x, y)$, $(y,z)$, and $(z, x)$.

https://open.kattis.com/problems/noonerizedspumbers
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

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll
#define vs vector<string>

#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    ll x, y, z;
    string op, eq;
    cin >> x >> op >> y >> eq >> z;

    vector<ll> ten(12);
    ll tmp = 1;
    f (i, 0, 12) {
        ten[i] = tmp;
        tmp *= 10;
    }

    for (int i = 1; i < 12; i++) {
        ll px = x / ten[i];
        if (px == 0) break;
        for (int j = 1; j < 12; j++) {
            ll py = y / ten[j];
            if (py == 0) break;
            ll nx = x % ten[i] + py * ten[i];
            ll ny = y % ten[j] + px * ten[j];
            if (op == "*") {
                if ((nx * ny) == z) {
                    cout << nx << " * " << ny << " = " << z << '\n';
                    return 0;
                }
            } else {
                if ((nx + ny) == z) {
                    cout << nx << " + " << ny << " = " << z << '\n';
                    return 0;
                }
            }
        }
    }

    for (int i = 1; i < 12; i++) {
        ll px = x / ten[i];
        if (px == 0) break;
        for (int j = 1; j < 12; j++) {
            ll pz = z / ten[j];
            if (pz == 0) break;
            ll nx = x % ten[i] + pz * ten[i];
            ll nz = z % ten[j] + px * ten[j];
            if (op == "*") {
                if ((nx * y) == nz) {
                    cout << nx << " * " << y << " = " << nz << '\n';
                    return 0;
                }
            } else {
                if ((nx + y) == nz) {
                    cout << nx << " + " << y << " = " << nz << '\n';
                    return 0;
                }
            }
        }
    }

    for (int i = 1; i < 12; i++) {
        ll py = y / ten[i];
        if (py == 0) break;
        for (int j = 1; j < 12; j++) {
            ll pz = z / ten[j];
            if (pz == 0) break;
            ll ny = y % ten[i] + pz * ten[i];
            ll nz = z % ten[j] + py * ten[j];
            if (op == "*") {
                if ((x * ny) == nz) {
                    cout << x << " * " << ny << " = " << nz << '\n';
                    return 0;
                }
            } else {
                if ((x + ny) == nz) {
                    cout << x << " + " << ny << " = " << nz << '\n';
                    return 0;
                }
            }
        }
    }
}
```
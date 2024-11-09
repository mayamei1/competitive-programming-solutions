---
tags:
  - competitive-programming/judges/kattis
name: Quadratic Dissonance
date: 2023-04-05
---
#competitive-programming/binary-search
## _Solution:_
Binary search the answer. Could have used [[Binary Search#Ternary Search|ternary search]], but used derivatives instead.

https://open.kattis.com/problems/quadraticdissonance
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <queue>
#include <stack>
#include <map>
#include <set>
#include <limits>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>

using namespace std;

int main() {
    double a,b,c,d;
    cin >> a >> b >> c >> d;

    double delta = 0.000001;
    double h = 600,l = -600,m = 0, old_m = 1000;

    while (abs(m-old_m) > delta) {
        old_m = m;
        double f = m*m+a*m+b;
        double df = 2*m+a;
        double g = m*m+c*m+d;
        double dg = 2*m+c;

        double higher, dhigher;
        if (f > g) {
            higher = f;
            dhigher = df;
        } else if (f < g) {
            higher = g;
            dhigher = dg;
        } else if (abs(df) < abs(dg)) {
            higher = f;
            dhigher = df;
        } else {
            higher = g;
            dhigher = dg;
        }

        // go left
        if (dhigher > 0) {
            h=m;
            m=(h-l)/2+l;
        } else if (dhigher < 0) {
            l=m;
            m=(h-l)/2+l;
        }
    }

    cout << m << ' ' << max(m*m+a*m+b, m*m+c*m+d);
}
```
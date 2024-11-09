---
tags:
  - competitive-programming/judges/kattis
name: Menger Sponge
date: 2024-10-05
---
#competitive-programming/math 
## _Solution:_
This problem is very similar to the Cantor set. Iterate from $1\dots L$. For each dimension, multiply the numerator by $3$. Then, the fraction should be between $0\le x\le 3$. If at least two out of the three dimensions are $1<x<2$, then they fall into an empty square. Otherwise, for each dimension, modulo the numerator by the denominator (essentially discarding the whole number part of the fraction), then move onto the next iteration.

https://open.kattis.com/problems/mengersponge
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = int;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

bool c1(ii x) {
    int t = 3 * x.first;
    return x.second < t && t < (2 * x.second);
}

void up(ii& x) {
    x.first *= 3;
    x.first %= x.second;
}

void solve() {
    int l;
    ii x, y, z;
    cin >> l >> x.first >> x.second >> y.first >> y.second >> z.first >> z.second;

    for (int i = 0; i < l; i++) {
        int fail = c1(x) + c1(y) + c1(z);
        if (fail >= 2) {
            cout << 0 << endl;
            return;
        }
        
        up(x);
        up(y);
        up(z);

    }
    
    cout << 1 << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
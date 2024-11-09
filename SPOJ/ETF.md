---
tags:
  - competitive-programming/judges/spoj
name: Euler Totient Function
date: 2024-09-20
---
#competitive-programming/math/number-theory/eulers-phi 
## _Solution:_
Simply implement Euler's phi function's sieve.

https://www.spoj.com/problems/ETF/
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

vi primes;
vector<bool> comp;
vi phi;
void sieve_phi(int n) {
    comp.assign(n + 1, false);
    phi.assign(n + 1, 0);
    phi[1] = 1;
    primes.clear();
    for (int i = 2; i <= n; i++) {
        if (!comp[i]) {
            phi[i] = i - 1;
            primes.push_back(i);
        }
        for (auto p : primes) {
            if (i * p > n) break;
            comp[i * p] = true;
            if (i % p) {
                phi[i * p] = phi[i] * phi[p];
            } else {
                phi[i * p] = p * phi[i];
            }
        }
    }
}

void solve() {
    int n;
    cin >> n;
    cout << phi[n] << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve_phi(1e6);

    int t;
    cin >> t;

    while (t--) solve();
}
```
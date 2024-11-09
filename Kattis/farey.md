---
tags:
  - competitive-programming/judges/kattis
name: Farey Sequence Length
date: 2024-09-20
---
#competitive-programming/math/number-theory/eulers-phi #competitive-programming/ds/range-query/running-sum 
## _Solution:_
For a fixed $b$, the number of co-prime $a$'s can be found via Euler's phi function. Then, we can use a prefix sum to calculate for all $b$. Be sure to add 1 to the end, since we need to include $0/1$.

https://open.kattis.com/problems/farey
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
    int k, n;
    cin >> k >> n;
    cout << k << ' ' << phi[n] + 1 << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve_phi(1e6);
    for (int i = 1; i <= 1e6; i++) {
        phi[i] += phi[i - 1];
    }

    int t;
    cin >> t;

    while (t--) solve();
}
```
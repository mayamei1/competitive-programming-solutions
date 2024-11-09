---
tags:
  - competitive-programming/judges/kattis
name: Cracking RSA
date: 2024-11-05
---
#competitive-programming/math/number-theory/eulers-phi 
## _Solution:_
Observe that since $p$ and $q$ are at most $1000$, then $n\le1000000$. Thus, we can calculate the totient function up to $10^{6}$. Then, for each $(n,e)$, we can find $\phi(n)$ and try every $d=1,\dots,n-1$ and check if $de\equiv1\mod\phi(n)$.

https://open.kattis.com/problems/crackingrsa
```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;
using dd = int;
using vi = vector<dd>;
using vvi = vector<vi>;
using ii = pair<dd,dd>;
using vii = vector<ii>;
using vvii = vector<vii>;

vi primes;
vector<bool> comp;
vi phi;
void sieve(int n) {
    comp.assign(n + 1, false);
    phi.assign(n + 1, 0);
    primes.clear();
    
    phi[1] = 1;
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
                break;
            }
        }
    }
}

void solve() {
    ll n, e;
    cin >> n >> e;
    ll tot = phi[n];

    for (int d = 1; d < tot; d++) {
        ll m = (1ll * d * e) % tot;
        if (m == 1) cout << d << endl;
    }
}

int main() {
    sieve(1000000);

    int t;
    cin >> t;

    while (t--) solve();
}
```
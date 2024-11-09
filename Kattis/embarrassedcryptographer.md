---
tags:
  - competitive-programming/judges/kattis
name: Embarrassed Cryptographer
date: 2024-09-20
---
#competitive-programming/math/number-theory/sieve #competitive-programming/math/modular-arithmetic #competitive-programming/long-division
## _Solution:_
Use sieve to find primes up to $10^6$. Then iterate through each prime smaller than $l$ and check if $k$ is divisible. Since $k$ can be large, you *should have* been able to simply do long division by checking each character in $k$. However, the time limit is extremely strict, so you must group characters together into chunks and perform the long division on those chunks. This should cut the time since there are less modulo operations being done.

https://open.kattis.com/problems/embarrassedcryptographer
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = ll;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

vi primes;
vector<bool> comp;
void sieve_primes(int n) {
    comp.assign(n + 1, false);
    primes.clear();
    for (int i = 2; i <= n; i++) {
        if (!comp[i]) primes.push_back(i);
        for (auto p : primes) {
            if (i * p > n) break;
            comp[i * p] = true;
            if (i % p == 0) break;
        }
    }
}

ll pow10[19];

bool solve() {
    string ks;
    int l;
    cin >> ks >> l;
    if (ks == "0" && l == 0) return false;

    vii k;
    ll d = 0;
    ll len = 0;
    for (char c : ks) {
        d = (d * 10 + (c - '0'));
        len++;
        if (len == 17) {
            k.push_back({d, len});
            d = 0;
            len = 0;
        }
    }
    if (len) k.push_back({d, len});

    for (int p : primes) {
        if (p >= l) break;
        ll rem = 0;
        for (auto [d, len] : k) {
            rem = (((rem % p) * (pow10[len] % p) % p) + (d % p)) % p;
        }
        
        if (rem == 0) {
            cout << "BAD " << p << endl;
            return true;
        }
    }
    cout << "GOOD" << endl;
    return true;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve_primes(1e6);
    pow10[0] = 1;
    for (int i = 1; i <= 18; i++) pow10[i] = 10 * pow10[i - 1];

    while(solve());
}
```
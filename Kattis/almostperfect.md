---
type:
  - competitive-programming
  - kattis
tags:
  - math/primes/prime-factors
name: Almost Perfect
---
## _Solution:_
Calculate the [[Primes#Sum of unique divisors|sum of unique divisors]] and calculate the difference of $sumDiv(n)$ and $n$.

https://open.kattis.com/problems/almostperfect
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

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll

using namespace std;

#define LSOne(S) ((S) & -(S))

ll _sieve_size;
bitset<10000010> bs;
vector<ll> p;

void sieve(ll upper_bound) {
    _sieve_size = upper_bound + 1;
    bs.set();
    bs[0] = 0; bs[1] = 0;
    for (ll i = 2; i < _sieve_size; i++) {
        if (!bs[i]) continue;
        for (ll j = i * i; j < _sieve_size; j += i) bs[j] = 0;
        p.push_back(i);
    }
}

bool is_prime(ll n) {
    if (n < _sieve_size) return bs[n];
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++)
        if (n % p[i] == 0) return false;
    return true; // works for (last prime)^2
}

ll bin_pow(ll n, ll k) {
    ll res = 1;
    while (k) {
        if (k & 1) res *= n;
        n *= n;
        k >>= 1;
    }
    return res;
}

ll prime_factors(ll n) {
    ll ans = 1;
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++) {
        ll count = 0;
        while (n % p[i] == 0) {
            n /= p[i];
            count++;
        }
        ans *= (bin_pow(p[i], count + 1) - 1) / (p[i] - 1);
    }
    if (n != 1) ans *= (bin_pow(n, 2) - 1) / (n - 1);
    return ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(10000000);

    int n;

    while (cin >> n) {
        ll val = abs(prime_factors(n) - 2 * n);
        cout << n;
        if (val == 0) cout << " perfect\n";
        else if (val <= 2) cout << " almost perfect\n";
        else cout << " not perfect\n";
    }
}
```
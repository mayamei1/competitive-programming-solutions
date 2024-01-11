---
type:
  - competitive-programming
  - kattis
tags:
  - math/primes/prime-factors
  - trivial
name: Jazz it Up!
---
## _Solution:_
Get all primes within 100000 (or some other reasonable number that is large enough to have primes that work for every $n$). Then iterate through every prime and check if $n\mod{m}\neq 1$.

https://open.kattis.com/problems/jazzitup
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

vector<ll> prime_factors(ll n) {
    vector<ll> factors;
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++) {
        while (n % p[i] == 0) {
            n /= p[i];
            factors.push_back(p[i]);
        }
    }
    if (n != 1) factors.push_back(n);
    return factors;
}

ll euler_phi(ll n) {
    ll ans = n;
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++) {
        if (n % p[i] == 0) ans -= ans / p[i];
        while (n % p[i] == 0) n /= p[i];
    }
    if (n != 1) ans -= ans / n;
    return ans;
}

int vp(int p, int n) { // legendre's formula (highest power of prime p that can divide n!)
    int ans = 0;
    for (int i = p; i <= n; i *= p)
        ans += n / i;
    return ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(1000000);

    int n;
    cin >> n;

    for (int prime : p) {
        if (n % prime) {
            cout << prime;
            break;
        }
    }
}
```
---
tags:
  - competitive-programming/catalog/kattis
name: Divisors
---
#competitive-programming/math/primes/prime-factors
#competitive-programming/math/combinatorics
## _Solution:_
Pre-calculate and store the prime factors of $1!,2!,\dots,431!$ in the form of $n!=a^i+b^j+\cdot+c^k$. For each query, find $_nC_k$ by adding/subtracting prime frequencies of each factorial, then calculate [[Primes#Number of unique divisors|the number of unique divisors]].

https://open.kattis.com/problems/divisors
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

vector<unordered_map<ll, int>> pf(432);
void prime_factors(ll n) {
    int nn = n;
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++) {
        while (n % p[i] == 0) {
            n /= p[i];
            pf[nn][p[i]]++;
        }
    }
    if (n != 1) pf[nn][n]++;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(10000000);

    for (int i = 2; i <= 431; i++) {
        pf[i] = pf[i - 1];
        prime_factors(i);
    }

    ll n, k;

    while (cin >> n >> k) {
        // n! / (n - k)!k!

        unordered_map<ll, int> nck = pf[n];
        for (auto p : pf[n - k]) {
            nck[p.first] -= p.second;
        }
        for (auto p : pf[k]) {
            nck[p.first] -= p.second;
        }

        ll ans = 1;
        for (auto p : nck) {
            ans *= (p.second + 1);
        }

        cout << ans << '\n';
    }
}
```
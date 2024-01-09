---
type:
  - competitive-programming
  - kattis
tags:
  - math/primes/prime-factors
---
#kattis #kattis-primalrepresentation

## _Solution:_
Get prime factors in prime factor exponential form

https://open.kattis.com/problems/primalrepresentation
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

unordered_map<ll, int> prime_factors(ll n) {
    unordered_map<ll, int> factors;
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++) {
        while (n % p[i] == 0) {
            n /= p[i];
            factors[p[i]]++;
        }
    }
    if (n != 1) factors[n]++;
    return factors;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(10000000);

    int n;

    while (cin >> n) {
        bool negative = false;
        if (n < 0) {
            n = -n;
            negative = true;
        }

        unordered_map<ll, int> freq = prime_factors(n);
        map<ll, int> ordered_freq;
        for (auto pf : freq) {
            ordered_freq.insert(pf);
        }

        if (negative) cout << "-1 ";
        for (auto pf : ordered_freq) {
            if (pf.second == 1) {
                cout << pf.first << ' ';
            } else {
                cout << pf.first << '^' << pf.second << ' ';
            }
        }

        cout << '\n';
    }
}
```
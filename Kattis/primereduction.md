---
type:
  - competitive-programming
  - kattis
tags:
  - math/primes/prime-factors
  - simulation
name: Prime Reduction
---
## _Solution:_
Simulate repeatedly checking prime and summing prime factors.

https://open.kattis.com/problems/primereduction
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

ll prime_factors(ll n) {
    ll sum = 0;
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++) {
        while (n % p[i] == 0) {
            n /= p[i];
            sum += p[i];
        }
    }
    if (n != 1) sum += n;
    return sum;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(10000000);

    int n;

    while (cin >> n && n != 4) {
        int count = 1;
        while (!is_prime(n)) {
            n = prime_factors(n);
            count++;
        }

        cout << n << ' ' << count << '\n';
    }
}
```
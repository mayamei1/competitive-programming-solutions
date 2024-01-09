---
type:
  - competitive-programming
  - kattis
tags:
  - math/primes/sieve
---
#kattis #kattis-englarginghashtables

## _Solution:_
Iterate through every number greater than $2n$ and check primality. Also check for $n$'s primality.

https://open.kattis.com/problems/enlarginghashtables
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

void prime_factors(ll n, unordered_map<ll, ll>& factors) {
    for (int i = 0; i < (int)p.size() && p[i]*p[i] <= n; i++) {
        while (n % p[i] == 0) {
            n /= p[i];
            factors[p[i]]++;
        }
    }
    if (n != 1) factors[n]++;
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
    
    sieve(10000000);

    ll n;
    
    while (cin >> n && n != 0) {
        bool n_prime = is_prime(n);

        ll i = n * 2 + 1;
        while (true) {
            if (is_prime(i)) {
                cout << i;
                if (!n_prime) cout << " (" << n << " is not prime)";
                cout << '\n';
                break;
            }
            i++;
        }
    }
}
```
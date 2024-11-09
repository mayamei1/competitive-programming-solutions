---
tags:
  - competitive-programming/judges/kattis
name: "Goldbach's Conjecture"
date: 2023-09-21
---
#competitive-programming/math/number-theory/sieve
## _Solution:_
Pre-calculate prime numbers, then for each query, check increasingly larger primes if $x-p_i$ is prime until it goes over half of $x$.

https://open.kattis.com/problems/goldbach2
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

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

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

int n, x;
vii ans;

void solve() {
    int i = 0, e = (x + 1) / 2;
    ans = vii();
    while (true) {
        if (p[i] > e) break;
        if (p[i] && is_prime(x - p[i])) ans.push_back({p[i], x - p[i]});
        i++;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(32001);

    cin >> n;

    while (n--) {
        cin >> x;
        solve();

        cout << x << " has " << ans.size() << " representation(s)\n";
        
        for (ii a : ans) {
            cout << a.first << '+' << a.second << '\n';
        }
        cout<< '\n';
    }
}
```
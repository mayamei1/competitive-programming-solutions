---
tags:
  - competitive-programming/judges/codechef
name: Number Hunt
date: 2024-07-10
---
#competitive-programming/math/number-theory/sieve #competitive-programming/greedy
## _Solution:_
$Y$ must be the product of the smallest two primes that are greater than or equal to $X$. Thus, you can greedily iterate starting from $X$ to find the first two occurring primes. The distance between primes for $10^9$ is very small, so most of the time complexity comes from checking if a value is prime or not.

https://www.codechef.com/problems/NUMHUNT
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd int
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

using namespace std;

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

void solve() {
    ll x;
    cin >> x;

    ll p1 = x;
    while (!is_prime(p1)) p1++;
    ll p2 = p1 + 1;
    while (!is_prime(p2)) p2++;

    cout << (p1 * p2) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(1e6);

    int t;
    cin >> t;

    while (t--) solve();
}
```
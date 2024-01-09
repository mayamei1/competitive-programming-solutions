---
type:
  - competitive-programming
  - kattis
tags:
  - math/primes/sieve
---
#kattis #kattis-primesieve

## _Solution:_
Prime sieve, nothing extra or MLE.

https://open.kattis.com/problems/primesieve
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
bitset<100000010> bs;

void sieve(ll upper_bound) {
    _sieve_size = upper_bound + 1;
    bs.set();
    bs[0] = 0; bs[1] = 0;
    for (ll i = 2; i < _sieve_size; i++) {
        if (!bs[i]) continue;
        for (ll j = i * i; j < _sieve_size; j += i) bs[j] = 0;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, q;
    cin >> n >> q;

    sieve(n + 1);

    ll c = 0;
    for (int i = 2; i <= n; i++) {
        if (bs[i]) c++;
    }

    cout << c << '\n';

    for (int i = 0; i < q; i++) {
        ll x;
        cin >> x;

        if (bs[x]) cout << "1\n";
        else cout << "0\n";
    }
}
```
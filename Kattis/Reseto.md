---
type:
  - competitive-programming
  - kattis
tags:
  - math/primes/sieve
---
#kattis #kattis-reseto

## _Solution:_
Prime sieve, but keep track of number of unique non-primes during sieve.

https://open.kattis.com/problems/reseto
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

int sieve(ll upper_bound, int k) {
    _sieve_size = upper_bound + 1;
    bs.set();
    bs[0] = 0; bs[1] = 0;
    for (ll i = 2; i < _sieve_size; i++) {
        if (!bs[i]) continue;
        k--;
        if (k == 0) return i;
        for (ll j = i * i; j < _sieve_size; j += i) {
            if (bs[j] == 1) {
                bs[j] = 0;
                k--;
                if (k == 0) return j;
            }
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, k;
    cin >> n >> k;

    cout << sieve(n, k);
}
```
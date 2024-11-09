---
tags:
  - competitive-programming/judges/kattis
name: Low Order Zeros
date: 2023-08-04
---
#competitive-programming/math/number-theory/primes
#competitive-programming/math/modular-arithmetic
#competitive-programming/math/factorials
## _Solution:_
Observe that the number of $0$ in the factorial is the minimum of factors of $2$ or $5$. When looking at the prime factorizations, we need a pair of $2$ and $5$ to get a low-order $0$ digit.

Calculate factorials iteratively. Each iteration keeps track of number of $2$ and $5$ factors of the current factorial and the least significant digit (modulo 10) of the factorial with the factors of $2$ and $5$ removed (let's call that $curr$).

To calculate the answer of the current iteration, figure out how many $2$s or $5$s can not be paired, and multiply them into $curr$ while performing modular arithmetic to keep the least significant digit. The values of $2^n$ and $5^n$ can be calculated with binary exponentiation. The algorithm can then be modified to also perform modular arithmetic.

Pre-calculate the values, then process the queries.

https://open.kattis.com/problems/loworderzeros
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

ll bin_pow(ll n, ll k, ll m) {
    n %= m;
    ll res = 1;
    while (k) {
        if (k & 1) {
            res = (res * n) % m;
        }
        n = (n * n) % m;
        k >>= 1;
    }
    return res;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int no2 = 0, no5 = 0;
    int curr = 1;

    vi ans(1000001);
    for (int i = 1; i <= 1000000; i++) {
        int temp = i;
        while (temp % 2 == 0) {
            no2++;
            temp /= 2;
        }
        while (temp % 5 == 0) {
            no5++;
            temp /= 5;
        }
        curr = (curr * (temp % 10)) % 10;
        
        if (no2 > no5) ans[i] = (curr * bin_pow(2, no2 - no5, 10)) % 10;
        else ans[i] = (curr * bin_pow(5, no5 - no2, 10)) % 10;
    }

    int n;
    while (cin >> n && n) {
        cout << ans[n] << '\n';
    }
}
```
---
tags:
  - competitive-programming/judges/kattis
name: LCM Pair Sum
date: 2024-02-17
---
#competitive-programming/math/combinatorics
#competitive-programming/math/gcd
## _Solution:_
Lets call each prime power $a_i=p_i{}^{n_i}$. All possible combinations of LCMs for $a_i$ is every power of $p_i$ from $0\leq k<n_i$ paired with $a_i$, plus $a_i$ paired with itself. 
$$
f(a_i)=(p_i{}^0+a_i)+(p_i{}^1+a_i)+\cdots+(p_i{}^{n_i-1}+a_i)+(a_i+a_i)
$$

This equation can be modified to the following.
$$
f(a_i)=\sum\limits_{k=0}^{n_i-1}p_i{}^{k}+(n_i+1)a_i+a_i
$$
Simplifying the geometric sum to a value $g_i$ for a given $a_i$, if we want to solve for $a_ia_j$, we would need to pair $g_ig_j$ with $a_ia_j$, and pair $g_ia_j$ with $g_ja_i$, as well as some other missing pairs $m$.
$$
f(a_ia_j)=g_ig_j+a_ia_jn_in_j+g_ia_jn_j+g_ja_in_i+m
$$

If you imaging a grid, with each prime being its own axis, and the units being the powers of the primes, then the pairings are covering the cases for a particular point, and the outer edges or faces of these grids would be missing. Those outer faces in this case are $(a_ia_j,a_ia_j)$ and $(g_ia_j,g_ja_i)$. Thus, $m=a_ia_j+a_ia_j+g_ia_j+g_ja_i$, and we get
$$
\begin{align*}
f(a_ia_j)&=g_ig_j+a_ia_j(n_i+1)(n_j+1)+g_ia_j(n_j+1)+g_ja_i(n_i+1)+a_ia_j\\
&=[g_i+a_i(n_i+1)][g_j+a_j(n_j+1)]+a_ia_j
\end{align*}
$$
So, since we have $f(a_i)=[g_i+a_i(n_i+1)]+a_i$, and we set $h(a_i)=[g_i+a_i(n_{i}+1)]$, we get
$$f(a_ia_j)=h(a_i)h(a_j)+a_ia_j$$

You can continue this, and calculate $f(a_1a_{2}\cdots a_c)=h(a_{1})h(a_{2})\cdots h(a_{c})+a_{1}a_{2}\cdots a_{c}$.

https://open.kattis.com/problems/lcmpairsum
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
#include <iomanip>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll
#define vs vector<string>

#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

#define MOD 1000000007ll

ll mod(ll a) {
    return ((a % MOD) + MOD) % MOD;
}

ll bin_pow(ll n, ll k) {
    ll res = 1;
    while (k) {
        if (k & 1) res = mod(res * n);
        n = mod(n * n);
        k >>= 1;
    }
    return res;
}

ll inv(ll a) {
    return bin_pow(a, MOD-2);
}

ll geometric(ll r, ll n) {
    return mod(mod(bin_pow(r, n) - 1) * inv(r - 1));
}

#define vll vector<ll>

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int tc;
    cin >> tc;

    cf (i, 1, tc) {
        int c;
        cin >> c;

        ll ans = 1;
        ll p, n, a, g, v = 1;
        f (j, 0, c) {
            cin >> p >> n;
            a = bin_pow(p, n);
            g = geometric(p, n);

            ans = mod(ans * mod(g + mod(a * (n + 1))));

            v = mod(v * a);
        }
        cout << "Case " << i << ": " << mod(ans + v) << '\n';
    }
}
```
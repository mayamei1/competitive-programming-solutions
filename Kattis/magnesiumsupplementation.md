---
tags:
  - competitive-programming/judges/kattis
name: Magnesium Supplementation
date: 2024-01-29
---
#competitive-programming/math/factors
#competitive-programming/limit-reduction
## _Solution:_
Search $i$ between $1$ and $\sqrt{n}$, and check if $i$ is a factor of $n$. Check if $i$ or $n/i$ is at most $k$ in order to add to answer list.

https://open.kattis.com/problems/magnesiumsupplementation
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    ll n, k, p;
    cin >> n >> k >> p;

    set<ll> ans;

    for (ll i = 1; i * i <= n; i++) {
        if (n % i) continue;
        ll j = n / i;
        if (j <= p && i <= i) ans.insert(i);
        if (i <= p && j <= k) ans.insert(j);
    }

    cout << ans.size() << '\n';
    for (ll a : ans) {
        cout << a << '\n';
    }
}
```
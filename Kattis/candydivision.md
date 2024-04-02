---
tags:
  - competitive-programming/catalog/kattis
name: Candy Division
---
#competitive-programming/math/factors
#competitive-programming/limit-reduction
## _Solution:_
Search $i$ between $1$ and $\sqrt{n}$ and check if $i$ is a factor of $n$. If so, add $i$ and $n/i$ to an ordered set, or add to a list to be sorted at the end (accounting for duplicates). Print factors minus $1$.

https://open.kattis.com/problems/candydivision
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

    ll n;
    cin >> n;
    set<ll> ans;
    for (ll i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            ans.insert(i);
            ans.insert(n / i);
        }
    }

    for (ll a : ans) {
        cout << (a - 1) << ' ';
    }
}
```
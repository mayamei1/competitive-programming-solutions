---
tags:
  - competitive-programming/catalog/kattis
name: Neighborhood Watch
---
#competitive-programming/math/combinatorics
## _Solution:_
Start with assuming every pairs of houses are safe or $n\times(n+1)/2$. Then, for every continuous grouping of unsafe houses, subtract from the answer every pair between those houses (assuming the length of the group is $l$, subtract $l\times(l+1)/2$).

https://open.kattis.com/problems/neighborhoodwatch
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

    ll n, k;
    cin >> n >> k;

    if (k == 0) {
        cout << "0\n";
        return 0;
    }

    ll ans = n * (n + 1) / 2;
    ll h, p_h, diff;
    p_h = -1;
    f (i, 0, k) {
        cin >> h;
        h--;
        diff = h - p_h - 1;
        ans -= diff * (diff + 1) / 2;
        p_h = h;
    }
    diff = n - p_h - 1;
    ans -= diff * (diff + 1) / 2;

    cout << ans;
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Short Sell
date: 2024-04-04
---
#competitive-programming/greedy #competitive-programming/work-backwards 
## _Solution:_
Iterating backwards, keep track of the buying point. To do that, make sure to add $k$ for each iteration, but replace if it is better to buy at the current iteration.

https://open.kattis.com/problems/shortsell
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

#define ll long long int
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

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, k;
    cin >> n >> k;

    vi a(n);
    f (i, 0, n) {
        cin >> a[i];
    }

    int ans = 0;
    int buy = a.back() * 100;
    rf (i, n, 0) {
        buy += k;
        buy = min(buy, a[i]*100 + k);
        ans = max(ans, a[i]*100 - buy);
    }

    cout << ans << endl;
}
```
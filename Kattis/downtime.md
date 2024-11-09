---
tags:
  - competitive-programming/judges/kattis
name: Disastrous Downtime
date: 2024-03-04
---
Sort the timings of each start/end of a request. At each time, increment or decrement to keep track of the number of requests going on at a time. Make sure to do any potential decrements first if there are events of the same time. Then, do $\lfloor\frac{\max(\mathrm{requests})}{k}\rfloor$.
## _Solution:_

https://open.kattis.com/problems/downtime
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

    int n, k;
    cin >> n >> k;

    vii ev;
    f (i, 0, n) {
        int t;
        cin >> t;
        ev.push_back({t, 1});
        ev.push_back({t + 1000, -1});
    }

    sort(ev.begin(), ev.end());

    int ma = 0, cur = 0;
    for (ii e : ev) {
        cur += e.second;
        ma = max(ma, cur);
    }

    cout << ((ma + k - 1) / k);
}
```
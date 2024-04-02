---
tags:
  - competitive-programming/catalog/kattis
name: Perket
---
#competitive-programming/complete-search #competitive-programming/bitmask 
## _Solution:_
Solution 1: Iterate through bitmasks to try every combination of ingredients.
Solution 2: Recursive backtracking

https://open.kattis.com/problems/perket
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

    int n;
    cin >> n;

    vii a(n);
    f (i, 0, n) {
        cin >> a[i].first >> a[i].second;
    }

    int mask_n = 1 << n;
    ll mi = abs(a[0].first - a[0].second);
    f (i, 1, mask_n) {
        ll s = 1, b = 0;
        f (j, 0, n) {
            if (i & (1 << j)) {
                s *= a[j].first;
                b += a[j].second;
            }
        }
        mi = min(mi, abs(s - b));
    }

    cout << mi;
}
```
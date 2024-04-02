---
tags:
  - competitive-programming/catalog/kattis
name: Highest Hill
---
#competitive-programming/data-representation 
## _Solution:_
Get list of extremes, and calculate each peak and print largest.

https://open.kattis.com/problems/highesthill
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

    vector<ll> a;
    ll curr;
    cin >> curr;
    a.push_back(curr);
    cin >> curr;
    a.push_back(curr);
    int dir;
    if (a[0] == a[1]) dir = 0;
    else if (a[0] < a[1]) dir = 1;
    else dir = -1;
    f (i, 2, n) {
        cin >> curr;
        if (dir == 1 && a.back() < curr) {
            a.pop_back();
            a.push_back(curr);
        } else if (dir == -1 && a.back() > curr) {
            a.pop_back();
            a.push_back(curr);
        } else if (dir == 0 && a.back() != curr) {
            if (a.back() < curr) dir = 1;
            else dir = -1;
            a.pop_back();
            a.push_back(curr);
        } else if (dir == 1 && a.back() > curr) {
            dir = -1;
            a.push_back(curr);
        } else if (dir == -1 && a.back() < curr) {
            dir = 1;
            a.push_back(curr);
        }
    }

    ll ans = 0;
    for (int i = 1; i < a.size() - 1; i++) {
        ans = max(ans, a[i] - max(a[i - 1], a[i + 1]));
    }

    cout << ans;
}
```
---
tags:
  - competitive-programming/catalog/kattis
name: Killing Chaos
---
#competitive-programming/ds/disjoint-set #competitive-programming/data-representation #competitive-programming/work-backwards 
## _Solution:_
Working backwards, you can build up train segments. Using disjoint sets, you can keep track of the number of passengers for each segment. When a new coach is introduce, you can get the new chaos by figuring out the difference from the last chaos.

https://open.kattis.com/problems/killingchaos
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
#define dd ll
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

// find root (representative of group) of v
int find(vi &ds, int v) {
    // get root of n
    int root = v;
    while (ds[root] != -1) {
        root = ds[root];
    }

    // set every node in branch to have root as parent
    int idx = v;
    while (ds[idx] != -1) {
        int parent = ds[idx];
        ds[idx] = root;
        idx = parent;
    }

    return root;
}

// merge two trees/sets (root is r1)
void merge(vi& ds, int v, int u) {
    int r1 = find(ds, v);
    int r2 = find(ds, u);

    if (r1 != r2) {
        ds[r2] = r1;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    ll n;
    cin >> n;

    vi p(n + 1);
    cf (i, 1, n) {
        cin >> p[i];
    }

    vi a(n);
    rf (i, n, 0) {
        cin >> a[i];
    }

    ll ans = 0;
    ll cur = 0;
    ll seg = 0;
    umap<ll, ll> pas;
    vi ds(n + 2, -1);
    f (i, 0, n) {
        ll sub = 0;
        ll cnt = p[a[i]];
        seg++;

        if (pas.find(find(ds, a[i] - 1)) != pas.end()) {
            sub += (pas[find(ds, a[i] - 1)] + 9) / 10 * 10;
            cnt += pas[find(ds, a[i] - 1)];
            seg--;
        }

        if (pas.find(find(ds, a[i] + 1)) != pas.end()) {
            sub += (pas[find(ds, a[i] + 1)] + 9) / 10 * 10;
            cnt += pas[find(ds, a[i]  +1)];
            seg--;
        }

        cur += (cnt + 9) / 10 * 10 - sub;
        ans = max(ans, seg * cur);

        if (pas.find(find(ds, a[i] - 1)) != pas.end()) {
            merge(ds, a[i], a[i] - 1);
        }

        if (pas.find(find(ds, a[i] + 1)) != pas.end()) {
            merge(ds, a[i], a[i] + 1);
        }
        pas[find(ds, a[i])] = cnt;
    }

    cout << ans << endl;
}
```
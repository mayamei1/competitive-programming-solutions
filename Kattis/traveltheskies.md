---
tags:
  - competitive-programming/judges/kattis
name: Travel the Skies
date: 2024-02-14
---
#competitive-programming/simulation
## _Solution:_
Simulate :)

Note: Be weary of what $k$ and $n$ represent.

https://open.kattis.com/problems/traveltheskies
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

#define id pair<ll,ll>

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    ll k, n, m;
    cin >> k >> n >> m;

    vector<vector<vector<id>>> adj(n + 1, vector<vector<id>>(k + 1));
    f (i, 0, m) {
        ll u, v, d, z;
        cin >> u >> v >> d >> z;
        adj[d][u].push_back({v, z});
    }

    vector<vector<ll>> add(n + 1, vector<ll>(k + 1));
    f (i, 0, k*n) {
        ll a, b, c;
        cin >> a >> b >> c;
        add[b][a] = c;
    }

    vector<ll> cnt(k + 1);
    bool fail = false;
    cf (i, 1, n) {
        cf (j, 1, k) cnt[j] += add[i][j];
        cf (u, 1, k) {
            for (id v : adj[i][u]) {
                cnt[u] -= v.second;
                if (cnt[u] < 0) {
                    fail = true;
                    break;
                }
            }
            if (fail) break;
        }
        if (fail) break;
        cf (v, 1, k) {
            for (id u : adj[i][v]) {
                cnt[u.first] += u.second;
            }
        }
    }

    if (fail) cout << "suboptimal";
    else cout << "optimal";
}
```
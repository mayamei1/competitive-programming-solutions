---
type:
  - competitive-programming
  - ieeextreme
tags:
  - dp/classical
---
#ieeextreme 
## _Solution:_
A classical knapsack problem. DP states are which items to include up to ($i$) and capacity ($j$).
$$
dp[i][j]=\max{(dp[i-1][j], dp[i][j-1],dp[i-1][j-w_i]+f_i)}
$$

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

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

#define LSOne(S) ((S) & -(S))

int t, c, n;

vii g;
vvi dp;

int solve() {
    dp = vvi(n, vi(c + 1));

    int w = g[0].first, f = g[0].second;
    cf (i, w, c) {
        dp[0][i] = f;
    }

    f (i, 1, n) {
        w = g[i].first;
        f = g[i].second;
        cf (j, 0, c) {
            dp[i][j] = dp[i - 1][j];
            dp[i][j] = max(dp[i][j], dp[i][j - 1]);
            if (j - w >= 0) dp[i][j] = max(dp[i][j], dp[i - 1][j - w] + f);

        }
    }

    return dp[n - 1][c];
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> t;
    while (t--) {
        cin >> c >> n;
        g = vii(n);
        f (i, 0, n) {
            cin >> g[i].first >> g[i].second;
        }
        cout << solve() << '\n';
    }
}
```
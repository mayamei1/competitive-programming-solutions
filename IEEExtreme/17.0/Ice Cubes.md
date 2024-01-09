---
type:
  - competitive-programming
  - ieeextreme
tags:
  - dp
---
#ieeextreme 

## _Solution:_
Simple DP problem. DP states are current indices $(i,j)$ and number of **consecutive** "bad" coffee shops $K$. The table defaults to everything as "not visited" or a value of $-1$. After setting up base cases, you can iterate $(i,j)$ through a nested for loop, and a third nested loop for current $K$. If a particular state can be accessed, then $\mathrm{dp(i,j,k)}$ is the maximum based on the top and left cells.

There is also different DP behavior based on if the current location is a bad coffee shop. If it is, then for $k=1\dots K-1$,  $\mathrm{dp(i,j,k)}=\max{(\mathrm{dp(i-1,j,k-1)}, \mathrm{dp(i,j-1,k-1)})}$. If not, $k$ is $0$, but you need to iterate through all possible $k$ values for the top and left cells to find the maximum value.

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
int t, n, m, k, b;
vvi g;

int solve() {
    vector<vvi> dp(n, vvi(m, vi(k, -1)));
    if (g[0][0] < b) dp[0][0][1] = g[0][0];
    else dp[0][0][0] = g[0][0];

    int l = g[0][0] < b;
    f (i, 1, n) {
        if (g[i][0] < b) {
            l++;
            if (l == k) break;
            dp[i][0][l] = dp[i - 1][0][l - 1] + g[i][0];
        } else {
            dp[i][0][0] = dp[i - 1][0][l] + g[i][0];
            l = 0;
        }
    }

    l = g[0][0] < b;
    f (j, 1, m) {
        if (g[0][j] < b) {
            l++;
            if (l == k) break;
            dp[0][j][l] = dp[0][j - 1][l - 1] + g[0][j];
        } else {
            dp[0][j][0] = dp[0][j - 1][l] + g[0][j];
            l = 0;
        }
    }

    f (i, 1, n) {
        f (j, 1, m) {
            if (g[i][j] < b) {
                f (l, 1, k) {
                    dp[i][j][l] = max(dp[i - 1][j][l - 1], dp[i][j - 1][l - 1]);
                    if (dp[i][j][l] != -1) dp[i][j][l] += g[i][j];
                }
            } else {
                f (l, 0, k) {
                    dp[i][j][0] = max(dp[i][j][0], dp[i - 1][j][l]);
                    dp[i][j][0] = max(dp[i][j][0], dp[i][j - 1][l]);
                }
                if (dp[i][j][0] != -1) dp[i][j][0] += g[i][j];
            }
        }
    }

    int ans = dp[n - 1][m - 1][0];
    f (l, 1, k) {
        ans = max(ans, dp[n - 1][m - 1][l]);
    }
    return ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> t;
    cf (i, 1, t) {
        cin >> n >> m >> k >> b;
        g = vvi(n, vi(m));
        f (j, 0, n) {
            f (l, 0, m) {
                cin >> g[j][l];
            }
        }
        int result = solve();
        cout << "Case " << i << ": ";
        if (result == -1) cout << "IMPOSSIBLE";
        else cout << result;
        cout << endl;
    }
}
```
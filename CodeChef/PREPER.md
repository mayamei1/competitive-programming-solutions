---
tags:
  - competitive-programming/judges/codechef
name: Perfect Prefixes
date: 2024-07-03
---
#competitive-programming/dp #competitive-programming/permutation 
## _Solution:_
We can determine if a prefix is also a permutation by comparing the sum of the prefix to the corresponding triangle number. We will keep track of a DP table with state $i$ being the current position in the permutation, and $j$ denoting whether we are before, during, or after the operation. The DP recurrence can is different depending on $j$. For $j=0$ (before the operation), it is simply `dp[i][0]=dp[i-1][0] + sum[i] == tri[i]`, meaning we decide not to start doing the operation, and we add one if this prefix is equal to the triangle number. For $j=1$ (during the operation), we use `dp[i][1]=max(dp[i-2][0],dp[i-2][1]) + (sum[i - 2] + a[i] == tri[i - 1]) + (sum[i] == tri[i])`, meaning we want to pick the more optimal of continuing from the operation or starting the operation from two indices ago, and adding based on if the flipped of the last two elements are equal to their respective triangle number. Finally, for $j=2$ (after the operation), we can simply do `dp[i][2]=max(dp[i-1][0...2])+(sum[i]==tri[i])`, meaning we just take the most optimal of either never doing the operation, ending the operation, or after the operation at `i-1`, and add one if the sum is equal to the triangle number.

https://www.codechef.com/problems/PREPER
```cpp
#include <bits/stdc++.h>

#define ll long long
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

using namespace std;

const int N = 2e5 + 2;
int a[N];
int sum[N];
int tri[N];
int dp[N][3];

void solve() {
    int n;
    cin >> n;

    sum[0] = 0;
    tri[0] = 0;
    for (int i = 1; i <= n; i++) cin >> a[i], sum[i] = sum[i - 1] + a[i], tri[i] = tri[i - 1] + i;

    dp[0][0] = dp[0][1] = dp[0][2] = 0;
    dp[1][0] = dp[1][1] = dp[1][2] = (a[1] == 1);
    for (int i = 2; i <= n; i++) {
        dp[i][0] = dp[i - 1][0] + (sum[i] == tri[i]);
        dp[i][1] = max(dp[i - 2][0], dp[i - 2][1]) + (sum[i - 2] + a[i] == tri[i - 1]) + (sum[i] == tri[i]);
        dp[i][2] = max(dp[i - 1][0], max(dp[i - 1][1], dp[i - 1][2])) + (sum[i] == tri[i]);
    }

    cout << max(dp[n][0], max(dp[n][1], dp[n][2])) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}

```
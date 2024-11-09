---
tags:
  - competitive-programming/judges/kattis
name: Tri Tiling
date: 2021-11-01
---
#competitive-programming/dp 
## _Solution:_
Keep track of a two state DP, where $i$ is the current column, and $j$ are the different types of states at that column. Each state $j$ denotes filled or not filled for certain rows.

https://open.kattis.com/problems/tritiling
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <map>
#include <cmath>
#include <algorithm>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>

using namespace std;

int main() {
    vvi dp(33, vi(8));

    dp[0][0] = 1;

    for (int i = 0; i <= 30; i++) {
        dp[i + 2][0] += dp[i][0];
        dp[i + 1][1] += dp[i][0];
        dp[i + 1][4] += dp[i][0];

        dp[i + 1][0] += dp[i][1];
        dp[i + 1][6] += dp[i][1];

        dp[i + 1][4] += dp[i][3];

        dp[i + 1][0] += dp[i][4];
        dp[i + 1][3] += dp[i][4];

        dp[i + 1][1] += dp[i][6];
    }

    
    int n;
    while (cin >> n) {
        if (n == -1) break;
        cout << dp[n][0] << endl;
    }
}
```
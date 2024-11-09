---
tags:
  - competitive-programming/judges/kattis
name: Kinky Word Search
date: 2024-06-25
---
#competitive-programming/complete-search #competitive-programming/dp 
## _Solution:_
Complete search with DP. Keep track of a DP table with states $(cc,i,j,kk,d)$: $cc$ is current character in the word, $i$ and $j$ are row and column in the grid, $kk$ is the number of kinks, and $d$ is the direction of movement. If `dp[cc][i][j][kk][d]==true`, then you want to check every direction $nd$ to see if `grid[i][j]==word[cc+1]` and update `dp[cc][i][j][kk+(nd != d)][nd]=true`. Once the DP table is filled, check `dp[word.size() - 1][1..r][1...c][k][1...8]`to see if any are true.

https://open.kattis.com/problems/kinkywordsearch
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

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

const int R = 10 + 3;
const int N = 100 + 3;
// dp[cc][i][j][kk][d];
bool dp[N][R][R][N][8];
char grid[R][R];

int r, c;
int k; string s;

int moves[][2] = {
    {-1, -1},
    {0, -1},
    {1, -1},
    {-1, 1},
    {0, 1},
    {1, 1},
    {-1, 0},
    {1, 0},
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> r >> c;
    string s;
    memset(grid, 0, sizeof(grid));
    for (int i = 1; i <= r; i++) {
        for (int j = 1; j <= c; j++) {
            cin >> s;
            grid[i][j] = s[0];
        }
    }

    cin >> k >> s;

    if (k >= s.size()) {
        cout << "No" << endl;
        return 0;
    }

    memset(dp, false, sizeof(dp));

    for (int i = 1; i <= r; i++) {
        for (int j = 1; j <= c; j++) {
            for (int d = 0; d < 8; d++) {
                bool a = grid[i][j] == s[0];
                bool b = (s.size() == 1) || (grid[i+moves[d][0]][j+moves[d][1]] == s[1]);
                dp[0][i][j][0][d] = a && b;
            }
        }
    }

    int n = s.size();
    for (int cc = 1; cc < n; cc++) {
        for (int i = 1; i <= r; i++) {
            for (int j = 1; j <= c; j++) {
                for (int kk = 0; kk <= k; kk++) {
                    for (int d = 0; d < 8; d++) {
                        bool a = dp[cc - 1][i][j][kk][d];
                        for (int nd = 0; nd < 8; nd++) {
                            bool b = grid[i+moves[nd][0]][j+moves[nd][1]] == s[cc];
                            dp[cc][i+moves[nd][0]][j+moves[nd][1]][kk + (nd != d)][nd] |= a && b;
                        }
                    }
                }
            }
        }
    }

    for (int i = 1; i <= r; i++) {
        for (int j = 1; j <= c; j++) {
            for (int d = 0; d < 8; d++) {
                if (dp[n - 1][i][j][k][d]) {
                    cout << "Yes" << endl;
                    return 0;
                }
            }
        }
    }

    cout << "No" << endl;
}
```
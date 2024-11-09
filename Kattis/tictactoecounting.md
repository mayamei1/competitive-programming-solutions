---
tags:
  - competitive-programming/judges/kattis
name: Tic Tac Toe Counting
date: 2022-05-31
---
#competitive-programming/dp/recursive 
## _Solution:_
Pre-calculate every move with memoization.

https://open.kattis.com/problems/tictactoecounting
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

struct hash_vi {
    int operator()(const vi &v) const {
        int hash = v.size();
        for(auto &i : v) {
            hash ^= i + 0x9e3779b9 + (hash << 6) + (hash >> 2);
        }
        return hash;
    }
};

int check(vi& b) {
    if ((b[0] + b[1] + b[2]) == 3) return 1;
    if ((b[3] + b[4] + b[5]) == 3) return 1;
    if ((b[6] + b[7] + b[8]) == 3) return 1;
    if ((b[0] + b[3] + b[6]) == 3) return 1;
    if ((b[1] + b[4] + b[7]) == 3) return 1;
    if ((b[2] + b[5] + b[8]) == 3) return 1;
    if ((b[0] + b[4] + b[8]) == 3) return 1;
    if ((b[2] + b[4] + b[6]) == 3) return 1;
    if ((b[0] + b[1] + b[2]) == 12) return 2;
    if ((b[3] + b[4] + b[5]) == 12) return 2;
    if ((b[6] + b[7] + b[8]) == 12) return 2;
    if ((b[0] + b[3] + b[6]) == 12) return 2;
    if ((b[1] + b[4] + b[7]) == 12) return 2;
    if ((b[2] + b[5] + b[8]) == 12) return 2;
    if ((b[0] + b[4] + b[8]) == 12) return 2;
    if ((b[2] + b[4] + b[6]) == 12) return 2;
    return 0;
}

umap<vi, ii, hash_vi> dp;
void precalc(vi b, bool move) {
    if (dp.find(b) != dp.end()) return;

    int c = check(b);
    if (c == 1) {
        dp[b] = {1, 0};
        return;
    }
    if (c == 2) {
        dp[b] = {0, 1};
        return;
    }
    
    ii ans = {0, 0};
    f (i, 0, 9) {
        if (b[i] == 0) {
            b[i] = (move) ? 1 : 4;
            precalc(b, !move);
            ans.first += dp[b].first;
            ans.second += dp[b].second;
            b[i] = 0;
        }
    }
    dp[b] = ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    precalc(vi(9), true);

    int t;
    cin >> t;

    while (t--) {
        string s;
        cin >> s;

        vi b(9);
        f (i, 0, 9) {
            if (s[i] == 'X') b[i] = 1;
            else if (s[i] == 'O') b[i] = 4;
        }

        if (dp.find(b) == dp.end()) cout << "-1 -1" << endl;
        else cout << dp[b].first << ' ' << dp[b].second << endl;
    }
}
```
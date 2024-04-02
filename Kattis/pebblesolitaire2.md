---
tags:
  - competitive-programming/catalog/kattis
name: Pebble Solitaire
---
#competitive-programming/dp/recursive 
## _Solution:_
Try every possible move recursively, and pick the one with the lowest remaining pebbles. The answer of a board layout can be memoized. 

https://open.kattis.com/problems/pebblesolitaire2
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

bool idx(int b, int i) {
    return (b & (1 << i));
}

umap<int, int> dp;
int solve(int b) {
    if (dp.find(b) != dp.end()) return dp[b];

    int ans = 100000;
    bool fail = false;
    f (i, 1, 22) {
        if (!idx(b, i - 1) && idx(b, i) && idx(b, i + 1)) {
            int nb = b ^ (0b111 << (i - 1));
            ans = min(ans, solve(nb));
            fail = true;
        }
        if (idx(b, i - 1) && idx(b, i) && !idx(b, i + 1)) {
            int nb = b ^ (0b111 << (i - 1));
            ans = min(ans, solve(nb));
            fail = true;
        }
    }

    if (!fail) {
        ans = 0;
        f (i, 0, 23) {
            ans += idx(b, i);
        }
    }
    dp[b] = ans;
    return dp[b];
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) {
        string s;
        cin >> s;

        int b = 0;
        for (int i = 0; s[i]; i++) {
            b <<= 1;
            b = b | (s[i] == 'o');
        }

        cout << solve(b) << endl;
    }
}
```
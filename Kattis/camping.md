---
type:
  - competitive-programming
  - kattis
tags:
  - dp
  - dimension-splitting
  - ds/priority-queue
name: Nordic Camping
---
## _Solution:_
Use dynamic programming to get the largest square area into one corner of the square. Then spread the answer by row, then by column. To do that, (for one dimension) keep a priority queue that keeps track of size of square and index of that square, and sort by the largest square. Then, assign the location based on the largest square that is still in range. If the largest is not in range, keep popping out of priority queue until there  is a square that is in range.

https://open.kattis.com/problems/camping
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

    int n, m, q;
    cin >> n >> m;

    vector<string> map(n);
    f (i, 0, n) {
        cin >> map[i];
    }

    vvi dp(n, vi(m));
    // base cases
    f (i, 0, n) {
        dp[i][0] = map[i][0] == '.';
    }
    f (j, 1, m) {
        dp[0][j] = map[0][j] == '.';
    }

    f (i, 1, n) {
        f (j, 1, m) {
            if (map[i][j] == '#') {
                dp[i][j] = 0;
                continue;
            }

            dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]);
            dp[i][j] = min(dp[i][j], dp[i - 1][j - 1]);
            dp[i][j]++;
        }
    }

    priority_queue<ii> pq;
    f (i, 0, n) {
        rf (j, m, 0) {
            pq.push({dp[i][j], j});

            ii val;
            while (!pq.empty()) {
                val = pq.top();
                if (val.second - val.first >= j) pq.pop();
                else break;
            }

            dp[i][j] = val.first;
        }
        pq = priority_queue<ii>();
    }

    f (j, 0, m) {
        rf (i, n, 0) {
            pq.push({dp[i][j], i});

            ii val;
            while (!pq.empty()) {
                val = pq.top();
                if (val.second - val.first >= i) pq.pop();
                else break;
            }

            dp[i][j] = val.first;
        }
        pq = priority_queue<ii>();
    }

    cin >> q;
    f (i, 0, q) {
        int r, c;
        cin >> r >> c;
        r--; c--;
        cout << dp[r][c] * dp[r][c] << '\n';
    }
}
```
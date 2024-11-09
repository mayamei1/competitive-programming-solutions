---
tags:
  - competitive-programming/judges/ieeextreme
name: Ordered Permutations
date: 2023-10-28
---
#competitive-programming/math/combinatorics
#competitive-programming/dp
#competitive-programming/math/modular-arithmetic
#competitive-programming/permutation 
#competitive-programming/ds/range-query/running-sum 
## _Solution:_
Combinatorics problem using DP. Imagine building up the permutation one index at a time. Instead of being explicit about which values could be at a given location, think about where the next value in the permutation can be inserted. There are two states to keep track of: one for the index of the permutation you are trying to insert, and the previous iteration's possible insertion locations.

The DP table keeps track of the number of possible permutation that ends at a particular location during a particular index. As you iterate through each index, depending on the direction the rule is, you can keep a running sum of all possible permutations that would result in a particular location. After the final index, sum up all possible permutations at every location to get the answer.

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

ll p = 1000000007;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    string s;
    cin >> s;

    vector<ll> dp(1);
    dp[0] = 1;
    f (i, 1, n) {
        vector<ll> dp_next(i + 1, 0);
        
        if (s[i - 1] == '>') {
            ll run_sum = 0;
            rf (j, i, 0) {
                run_sum = (run_sum + dp[j]) % p;
                dp_next[j] = run_sum; 
            }
        } else {
            ll run_sum = 0;
            cf (j, 1, i) {
                run_sum = (run_sum + dp[j - 1]) % p;
                dp_next[j] = run_sum;
            }
        }

        dp.swap(dp_next);
    }

    ll count = 0;
    for (int i = 0; i < n; i++) {
        count = (count + dp[i]) % p;
    }
    cout << count;
}
```
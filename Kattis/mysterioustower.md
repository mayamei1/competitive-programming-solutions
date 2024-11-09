---
tags:
  - competitive-programming/judges/kattis
name: Mysterious Tower
date: 2024-05-22
---
#competitive-programming/dp #competitive-programming/math/probabilities
## _Solution:_
Observe that a stable tower represents a balanced set of parentheses/brackets, for example `(()())` or `()(())`. Now imagine that you are doing the $2^n$ solution where you try every possibility of `(` and `)` and also calculate the probabilities of each iteration. Now, imagine we wanted to add a new block with a probability of `(` or `)`. The iterations where the final height would increment by 1 is for those who have an "unclosed" -- there is no close bracket to go with it -- open bracket. Now, instead of representing each iteration as its own height and probability, we can instead group them together in a certain way to get the expected/average height and a total probability.

Let's say we have some $n$, and we can group the iterations by the number of unclosed open brackets. For example $n=3$ and $p=0.5,0.5,0.5$, we would group iterations in this way:

| # unclosed brackets | Iterations          | Probability |
| ------------------- | ------------------- | ----------- |
| 0                   | `)))`, `)()`, `())` | 0.375       |
| 1                   | `(()`, `))(`, `()(` | 0.375       |
| 2                   | `)((`               | 0.125       |
| 3                   | `(((`               | 0.125       |
With each grouping, we can keep track of the expected height across the iterations via a weighted average (the height of each iteration is multiplied by the probability of the iteration, summed, then divided by the sum of probabilities). Now, for the DP recurrence between $n$ and $n+1$, lets say you have the expected height and their probabilities of each group for $n$ and you are trying to add a new block with a probability $p$ of being a `(`. Let's think about the cases of groups where the number of unclosed opens are $o>0$. There are two ways of taking $n$ blocks and getting $n+1$ blocks and $o$ unclosed brackets: there was initially $o+1$ unclosed open brackets, and we added a close bracket, or there was initially $o-1$ and we added an open bracket. Every time we add a close bracket, the expected height is incremented by two (since we will now keep another pair of open and close brackets). In order to combine the two cases, since we have two expected heights and the probabilities, we can do a weighted average.  In the $o=0$ case, there are also two ways to get from $n$ to $n+1$ and $o=0$: initially there was $o=1$ and we added a close bracket (and increment the expected height by two), or there was initially $o=0$ and we added a close bracket (does not affect the height).
```python3
h1=dp[n][o+1].height + 2 # expected height of [n,o+1] + 2 for creating a new pair of ()
p1=dp[n][o+1].prob * (1-p[n+1]) # probability of [n,o+1] times probability of close bracket
h2=dp[n][o-1].height # expected height of [n,o-1]
p2=dp[n][o-1].prob * p[n+1] # probability of [n, o-1] times probability of open bracket
dp[n+1][o].height=(h1*p1+h2*p2)/(p1+p2) # weighted average
dp[n+1][o].prob=p1+p2 # total probability of [n+1,o]
```

Once you reach the desired length, do a final weighted average of $n$ to get the answer.

https://codesprintla24.kattis.com/contests/codesprintla24open/problems/mysterioustower
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

#define ll long long int
#define ull unsigned ll
#define vs vector<string>
#define dd double
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vi p(n);
    for (int i = 0; i < n; i++) {
        cin >> p[i];
    }


    vvii dp(n, vii(n + 2));
    dp[0][0] = {0, 1 - p[0]};
    dp[0][1] = {0, p[0]};
    for (int i = 1; i < n; i++) {
        double eh1 = dp[i - 1][0].first, eh2 = dp[i - 1][1].first + 2;
        double p1 = dp[i - 1][0].second * (1 - p[i]), p2 = dp[i - 1][1].second * (1 - p[i]);
        dp[i][0] = {(eh1 * p1 + eh2 * p2) / (p1 + p2), p1 + p2};
        for (int j = 1; j <= n; j++) {
            double eh1 = dp[i - 1][j - 1].first, eh2 = dp[i - 1][j + 1].first + 2;
            double p1 = dp[i - 1][j - 1].second * p[i], p2 = dp[i - 1][j + 1].second * (1 - p[i]);
            double prob = p1 + p2;
            if (prob == 0) continue;
            dp[i][j] = {(eh1 * p1 + eh2 * p2) / prob, prob};
        }
    }

    double ans = 0;
    for (int i = 0; i <= n; i++) {
        ans += dp[n - 1][i].first * dp[n - 1][i].second;
    }

    cout << ans << endl;
}
```
---
tags:
  - competitive-programming/judges/codechef
name: Maximum of GCDs
date: 2024-07-25
---
#competitive-programming/dp #competitive-programming/math/gcd #competitive-programming/ad-hoc/
## _Solution:_
It can be observed that for all subsegments that end with $r$, there are at most $O(\log{a_r})$ GCDs. Say we knew the GCD from $l$ to $r$. Then, the GCD from $l-1$ to $r$ is either equal (doesn't change number of GCDs), or at most half of the GCD from $l$ to $r$. Thus, there are at most $O(\log{a_r})$ unique GCDs. We can keep track of a DP table, where the states are $r$ and $g$, that keeps track of the maximum length of a subsegment that ends at $r$ with a GCD of $g$. Iterating through $r$, we can check every $g$ of $r-1$ and update values accordingly: `dp[r][gcd(g,a[r])]=max(dp[r][gcd(g,a[r])], dp[r-1][g] + 1)`. Then, we can check every $g$ at `dp[r]` and update the answer accordingly: for some `dp[r][g]=d`, `ans[d]=max(ans[d], g)`.

Then comes the question: is only updating the value at the maximum length for some GCD at some $r$ sufficient? The answer is yes. For some particular $r$ and $g$, there exists a range of $l$'s where $\gcd(a_{l\dots{r}})=g$. Say $l$ is the left most bound that provides a valid subsegment, and there exists $x>l$ that also provide valid subsegments. The length of the subsegment for $(x,r)$ is equal to the length of $(l,r-(x-l))$, and $\gcd(a_{l\dots{r}})=\gcd(a_{x\dots{r}})\le\gcd(a_{x\dots{r-(x-l)}})$. Thus, for any segments with equal GCDs that end at $r$ that isn't the maximal length, the same length segments could be checked with a different $r$ that would provide at least as good of an answer, if not better.

https://www.codechef.com/problems/KSIZEGCD
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = int;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

int gcd(int a, int b) {
    if(a == 0) return b;
    return gcd(b % a, a);
}

void solve() {
    int n;
    cin >> n;

    vi a(n);
    for (int& aa : a) cin >> aa;

    map<int, int> dp[n];
    dp[0][a[0]] = 0;
    vi ans(n);
    ans[0] = a[0];
    for (int i = 1; i < n; i++) {
        dp[i][a[i]] = 0;

        for (auto [g, l] : dp[i - 1]) {
            int& v = dp[i][gcd(g, a[i])];
            v = max(v, l + 1);
        }

        for (auto [g, l] : dp[i]) {
            ans[l] = max(ans[l], g);
        }
    }

    for (int a : ans) cout << a << ' ';
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Genius
date: 2024-10-21
---
#competitive-programming/dp #competitive-programming/math/probabilities #competitive-programming/math/modular-arithmetic 
## _Solution:_
Precalculate every guess. For each tournament, the probability of each player winning can be calculated by iterating through a bitmask up to $2^{3}-1$, where each bit denotes who wins certain match ups, and adding up probability of that particular event happening. Then, keep track of a two state DP table: $i$ denotes the checking tournament $1\dots i$, and $j$ denotes correctly guessing $j$ tournaments. Let's say for some $(i,j)$ that $g_{i}$ denotes the guess for round $i$, and $p_{i,k}$ denotes the probability that player $k$ wins. Then, the transition is `dp[i+1][j+1]+=dp[i][j]*prob[i][w[i]]` and `dp[i+1][j]+=dp[i][j]*(1-prob[w[i]])`. Then, the answer is the sum of $dp_{t,j}$ for $j=k\dots t$.

https://open.kattis.com/problems/genius
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = double;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

vi calc_prob(vi& w) {
    vi prob(4);
    int m_max = 1 << 3;
    for (int i = 0; i < m_max; i++) {
        int w1, w2, w3;
        double p;
        if (i & 1) {
            w1 = 0;
            p = (double)w[0] / (w[0] + w[1]);
        } else {
            w1 = 1;
            p = (double)w[1] / (w[0] + w[1]);
        }

        if (i & 2) {
            w2 = 2;
            p *= (double)w[2] / (w[2] + w[3]);
        } else {
            w2 = 3;
            p *= (double)w[3] / (w[2] + w[3]);
        }

        if (i & 4) {
            w3 = w1;
            p *= (double)w[w1] / (w[w1] + w[w2]);
        } else {
            w3 = w2;
            p *= (double)w[w2] / (w[w1] + w[w2]);
        }

        prob[w3] += p;
    }
    
    return prob;
}

void solve() {
    int k, t, p, q, x1;
    cin >> k >> t >> p >> q >> x1;

    vector<int> a = {x1};
    for (int i = 1; i < t; i++) a.push_back(a.back() * p % q);
    for (int& x : a) x %= 4;

    vvi dp(t + 1, vi(t + 1));
    dp[0][0] = 1;

    for (int i = 0; i < t; i++) {
        vi w(4);
        for (double& x : w) cin >> x;
        vi prob = calc_prob(w);
        for (int j = 0; j <= i; j++) {
            dp[i + 1][j + 1] += dp[i][j] * prob[a[i]];
            dp[i + 1][j] += dp[i][j] * (1 - prob[a[i]]);
        }
    }

    double ans = 0;
    for (int i = k; i <= t; i++) {
        ans += dp[t][i];
    }

    printf("%.9lf\n", ans);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
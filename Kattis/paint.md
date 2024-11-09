---
tags:
  - competitive-programming/judges/kattis
name: Paint
date: 2024-06-22
---
#competitive-programming/dp #competitive-programming/binary-search 
## _Solution:_
Keep track of a DP table with one state denoting the right most slat $s$ and keeps track of the maximum number of painted slats up to $s$. Since the number of states can be up to $10^{18}$, we will instead keep track of an ordered map. Sort the painters by their end slat. Iterate through each painter with start slat $a$ and end slat $b$, and consider two cases: (1) we include the current painter, and we search the DP table for the rightmost slat to the left of $a$, or (2) we don't include the current painter, and get the right most slat up to $b$. For the first case, you can binary search the keys in the map, and for the second case, you can simply keep track of the maximum value across iterations.

https://open.kattis.com/problems/paint
```cpp
#include <bits/stdc++.h>

#define ll long long
#define ull unsigned ll
#define vs vector<string>
#define dd ll
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

const int N = 2e5 + 2;
ii a[N];

bool comp(ii a, ii b) {
    if (a.second == b.second) return a.first < b.first;
    return a.second < b.second;
}

void solve() {
    ll n, k;
    cin >> n >> k;

    for (int i = 0; i < k; i++) {
        cin >> a[i].first >> a[i].second;
    }

    map<ll, ll> dp;
    dp[0] = 0;

    sort(a, a + k, comp);

    ll mx = 0;
    for (int i = 0; i < k; i++) {
        ll s = a[i].first, e = a[i].second;
        if (dp.find(e) == dp.end()) dp[e] = mx;
        auto itr = prev(dp.lower_bound(s));
        dp[e] = max(dp[e], itr->second + e - s + 1);
        mx = max(mx, dp[e]);
    }

    cout << (n - mx) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
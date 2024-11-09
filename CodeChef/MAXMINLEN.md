---
tags:
  - competitive-programming/judges/codechef
name: Max Min and Length
date: 2024-07-17
---
#competitive-programming/math/combinatorics #competitive-programming/math #competitive-programming/sorting 
## _Solution:_
Observe that sorting the array doesn't affect the answer. Also observe that good subsequences must consist of consecutive integers, except for one jump of size 2. If we change each element to $a_i-i$, we can keep track of groups of consecutive numbers, and jumps of size 2 now become jumps of size 1. Then, we can pick any size of jumps 1, and any consecutive groups to the left and the right are the potential starting and ending points of the sequence, so we can use product rule. Then, within groups of consecutive numbers, we can pick out a number to remove, then we have a jump of 1 again, which we perform the product rule again.

https://www.codechef.com/problems/MAXMINLEN
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

using namespace std;

void solve() {
    int n;
    cin >> n;

    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    sort(a.begin(), a.end());

    map<int, int> freq;
    for (int i = 0; i < n; i++) freq[a[i] - i]++;

    ll ans = 0;
    for (auto [v, f] : freq) {
        if (freq.count(v + 1)) ans += f * freq[v + 1];
    }

    for (auto [v, f] : freq) {
        for (ll m = 0; m < f; m++) {
            ans += m * (f - m - 1ll);
        }
    }
    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
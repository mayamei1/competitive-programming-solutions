---
tags:
  - competitive-programming/judges/atcoder
name: Count Arithmetic Subsequences
date: 2024-07-12
---
#competitive-programming/complete-search #competitive-programming/math/combinatorics #competitive-programming/dp 
## _Solution:_
In a DP like fashion, say we keep track of frequencies of different states $(d,l,s)$: $d$ being the common difference, $l$ as the last number in the sequence, and $s$ as the size of the sequence. Iterating through each element in $a_i$, we check every tuple $(d,l,s)$. If $s=1$, then you can add to that sequence no matter what, since a common difference has not been defined. If $a_i-l=d$, then we can also add to the sequence. Then, a new sequence can be generated with the current $a_i$.

https://atcoder.jp/contests/abc362/tasks/abc362_e
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

#define MOD 998244353

struct i3 {
    int dif, last, len;

    bool operator<(const i3& o) const {
        if (len != o.len) return len > o.len;
        if (dif != o.dif) return dif < o.dif;
        return last < o.last;
    }
};

const int N = 80 + 2;
int a[N];
int ans[N];

void solve() {
    int n;
    cin >> n;

    int inf = 1e9 + 7;
    for (int i = 0; i < n; i++) cin >> a[i];

    map<i3, int> freq;
    for (int i = 0; i < n; i++) {
        for (auto [s, f] : freq) {
            if (s.dif == inf) {
                int& t = freq[{a[i] - s.last, a[i], 2}];
                t = (t + f) % MOD;
            } else if (s.dif == a[i] - s.last) {
                int& t = freq[{s.dif, a[i], s.len + 1}];
                t = (t + f) % MOD;
            }
        }
        int& t = freq[{inf, a[i], 1}];
        t = (t + 1) % MOD;
    }

    memset(ans, 0, sizeof(ans));

    for (auto [s, f] : freq) {
        int& t = ans[s.len];
        t += f;
    }

    for (int i = 1; i <= n; i++) {
        cout << ans[i] << ' ';
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
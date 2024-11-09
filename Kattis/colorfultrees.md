---
tags:
  - competitive-programming/judges/kattis
name: Colorful Trees
date: 2024-10-05
---
#competitive-programming/ad-hoc/set-merging #competitive-programming/graph/tree #competitive-programming/math/combinatorics #competitive-programming/dp 
## _Solution:_
If we fix any vertex to be the root, we can find the answer in a DP-like fashion. Say for any vertex $u$, we knew the answer for all of its children, as well as the frequency of colors in the children's subtree. Then, we can perform set union by rank. Say the set with the largest rank is `mx`. Then, we can take the answer of the corresponding edge, and update the answer with each element we are merging in. Say we are merging $(c,f)$ denoting color $c$ with a frequency of $f$. Then, we subtract out the old `cnt[mx][c]*(total[c]-cnt[mx][c])`, update `cnt[mx][c]` to increment by $f$, then add in the new `cnt[mx][c]*(total[c]-cnt[mx][c]` to the answer.

https://open.kattis.com/problems/colorfultrees
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

vi c;
vi tot;
vvii adj;
vector<ll> ans;
vi root;
vector<map<int, int>> cnt;

void dfs(int u, int p, int i) {
    for (auto [v, i] : adj[u]) {
        if (v == p) continue;
        dfs(v, u, i);
    }

    ll sum = (tot[c[u]] - 1);
    int mx_r = u;
    for (auto [v, i] : adj[u]) {
        if (v == p) continue;
        int rv = root[v];
        if (cnt[rv].size() > cnt[mx_r].size()) mx_r = rv, sum = ans[i];
    }

    if (mx_r != u) {
        for (auto [c, f] : cnt[u]) {
            int& val = cnt[mx_r][c];
            sum -= 1ll * val * (tot[c] - val);
            val += f;
            sum += 1ll * val * (tot[c] - val);
        }
        root[u] = mx_r;
    }

    for (auto [v, i] : adj[u]) {
        if (v == p) continue;
        int rv = root[v];
        if (rv == mx_r) continue;
        for (auto [c, f] : cnt[rv]) {
            int& val = cnt[mx_r][c];
            sum -= 1ll * val * (tot[c] - val);
            val += f;
            sum += 1ll * val * (tot[c] - val);
        }
        root[rv] = mx_r;
    }

    ans[i] = sum;
}

void solve() {
    int n;
    cin >> n;

    c = vi(n + 1);
    tot = vi(n + 1);
    for (int i = 1; i <= n; i++) {
        cin >> c[i];
        tot[c[i]]++;
    }

    adj = vvii(n + 1);
    for (int i = 1; i < n; i++) {
        int u, v;
        cin >> u >> v;

        adj[u].push_back({v, i});
        adj[v].push_back({u, i});
    }

    root = vi(n + 1);
    cnt = vector<map<int, int>>(n + 1);
    for (int i = 1; i <= n; i++) {
        root[i] = i;
        cnt[i][c[i]]++;
    }

    ans = vector<ll>(n + 1);
    dfs(1, 0, 0);

    for (int i = 1; i < n; i++) {
        cout << ans[i] << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
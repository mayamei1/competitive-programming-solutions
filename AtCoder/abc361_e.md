---
tags:
  - competitive-programming/judges/atcoder
name: Tree and Hamiltonian Path 2
date: 2024-07-06
---
#competitive-programming/graph/tree/diameter #competitive-programming/greedy 
## _Solution:_
Find the max distance between any two nodes. You can then greedily start and end at those two nodes, resulting in the answer of two times the sum of all lengths minus the distance between the start and end.

https://atcoder.jp/contests/abc361/tasks/abc361_e
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

using namespace std;

const int N = 2e5 + 2;
vii adj[N];

ii dfs(int u, int p) {
    ii ans = {u, 0};

    for (auto [v, d] : adj[u]) {
        if (v == p) continue;
        ii o = dfs(v, u);
        o.second += d;
        if (o.second > ans.second) ans = o;
    }

    return ans;
}

void solve() {
    int n;
    cin >> n;

    ll sum = 0;
    for (int i = 1; i < n; i++) {
        int a, b, c;
        cin >> a >> b >> c;
        adj[a].push_back({b, c});
        adj[b].push_back({a, c});
        sum += c;
    }

    ii f = dfs(1, 0);
    ii s = dfs(f.first, 0);

    cout << (2 * sum - s.second) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
---
tags:
  - competitive-programming/judges/kattis
name: Island Alliances
date: 2024-06-24
---
#competitive-programming/ds/disjoint-set #competitive-programming/limit-reduction 
## _Solution:_
Use a disjoint-set to keep track of merging. Keep track of sets of invalid "root" islands for each "root" island. When merging, merge smaller sets into larger sets, as this amortizes the merge operation to $O(\log{n})$. Also, go through the smaller set's (let's say $r_b$) invalid root islands $r_i$ and remove $r_b$ from $r_i$'s sets and replace it with $r_a$, then finally add $r_i$ to $r_a$'s set.

https://open.kattis.com/problems/islandalliances
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

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

int n, m, q;

const int N = 2e5 + 2;
int root[N];
int cnt[N];
set<int> inv[N];

int find(int u) {
    int r = u;
    while (r != root[r]) r = root[r];
    while (u != r) {
        int tmp = root[u];
        root[u] = r;
        u = tmp;
    }
    return r;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n >> m >> q;

    for (int i = 1; i <= n; i++) {
        root[i] = i;
        cnt[i] = 1;
    }

    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        inv[u].insert(v);
        inv[v].insert(u);
    }

    for (int i = 0; i < q; i++) {
        int a, b;
        cin >> a >> b;

        int ra = find(a), rb = find(b);
        if (inv[ra].find(rb) != inv[ra].end()) {
            cout << "REFUSE" << endl;
            continue;
        }
        cout << "APPROVE" << endl;

        if (cnt[ra] > cnt[rb]) {
            root[rb] = ra;
            cnt[ra] += cnt[rb];
            for (int c : inv[rb]) {
                inv[c].erase(rb);
                inv[c].insert(ra);
                inv[ra].insert(c);
            }
        } else {
            root[ra] = rb;
            cnt[rb] += cnt[ra];
            for (int c : inv[ra]) {
                inv[c].erase(ra);
                inv[c].insert(rb);
                inv[rb].insert(c);
            }
        }
    }
}
```
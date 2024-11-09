---
tags:
  - competitive-programming/judges/codechef
name: Color Difference
date: 2024-07-03
---
#competitive-programming/data-representation #competitive-programming/ds/range-query/segment-tree 
## _Solution:_
Instead of representing the problem as the function $f(i,j)$, we can observe that for every distinct number $x$ in a range, we can count the number of ranges that do not include $x$. We can do so by finding every position of $x$, and checking ranges where $x$ does not exist if any there are any $M_i$ that are strictly within that range. Doing this for every $x$ can be done in a total $O(n\log(n))$. 

To do so, sort $M$ by the right boundary and keep track of the indices of the previous occurrence for each color $p(c)$. Iterate through $C_i$, and add the left boundaries of every $M_i$ where the right boundary is less than $i$ to a multiset. Alternatively, use a segment tree and add one at the left boundary. Then, binary search to find the number of elements larger than $p(C_i)$ and add that number to a counter for each color $d_c$.

To find the sum of $d_c$ for distinct colors in a particular range, you can once again use the sorted $M$ and $p(c)$, as well as a segment tree. Iterate through $C_i$, and subtract out $d_c$ from $p(C_i)$ from the segment tree and add in $d_c$ at $C_i$. Then, we can find the answer for $M_i$'s where the right boundary is at $i$ by querying $M_i$'s range.

https://www.codechef.com/problems/COLDIF
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

// bit(n+1)
void add(vi& bit, int i, long delta) {
    for (++i; i < bit.size(); i += (i & (-i))) {
        bit[i] += delta;
    }
}

ll sum(vi& bit, int i) {
    ll val = 0;
    for (++i; i > 0; i -= (i & (-i))) {
        val += bit[i];
    }
    return val;
}

ll sum(vi& bit, int l, int r) {
    return sum(bit, r) - ((l) ? sum(bit, l - 1) : 0ll);
}

bool comp(pair<ii, int> f, pair<ii, int> s) {
    return f.first.second < s.first.second;
}

void add_query(vvii& q, int l, int r, int c) {
    if ((r - l) <= 1) return;
    q[r - 1].push_back({l + 1, c});
}

void solve() {
    int n, m;
    cin >> n >> m;

    vi a(n + 1);
    for (int i = 1; i <= n; i++) cin >> a[i];

    vvii b(n + 1);
    for (int i = 0; i < m; i++) {
        int l, r;
        cin >> l >> r;
        b[r].push_back({l, i});
    }

    vvi idx(n + 1);
    for (int i = 1; i <= n; i++) {
        idx[a[i]].push_back(i);
    }

    vvii q(n + 1);
    for (int c = 1; c <= n; c++) {
        auto& idc = idx[c];
        if (idc.empty()) continue;
        add_query(q, 0, idc[0], c);
        for (int i = 1; i < idc.size(); i++) {
            add_query(q, idc[i - 1], idc[i], c);
        }
        add_query(q, idc.back(), n + 1, c);
    }

    vi bit(n + 2);
    vi cnt(n + 1);
    for (int r = 1; r <= n; r++) {
        for (auto [l, i] : b[r]) add(bit, l, 1);
        for (auto [l, c] : q[r]) cnt[c] += sum(bit, l, r);
    }

    bit = vi(n + 2);
    vi ans(m);
    vi prev(n + 1, -1);
    for (int r = 1; r <= n; r++) {
        int c = a[r];
        if (prev[c] != -1) add(bit, prev[c], -cnt[c]);
        prev[c] = r;
        add(bit, r, cnt[c]);
        for (auto [l, i] : b[r]) ans[i] = sum(bit, l, r);
    }

    for (ll a : ans) {
        cout << a << ' ';
    }
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
---
tags:
  - competitive-programming/judges/kattis
name: Triangular Logs
date: 2024-11-06
---
#competitive-programming/segment-tree #competitive-programming/coordinate-compression #competitive-programming/limit-reduction #competitive-programming/math/pigeon-hole 
## _Solution:_
We can observe that in order to a list of elements to fail, it must at minimum follow the Fibonacci sequence. And since the logs can be at most $10^{9}$, if there are 100 elements, it is guaranteed to pass. Thus, we can keep track of a coordinate compressed 2D segment tree, where each node keeps track of elements (up to 100).

https://open.kattis.com/problems/triangularlogs
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

vvi a;
void merge(vi& src, vi& des) {
    for (int x : src) {
        if (des.size() >= 100) break;
        des.push_back(x);
    }
}

struct segtree1 {
    vi li;
    vvi t;
    int n;
    
    int idx(int y) {
        return lower_bound(li.begin(), li.end(), y) - li.begin();
    }

    void init(int l, int r) {
        for (int i = l; i < r; i++) li.push_back(a[i][1]);
        sort(li.begin(), li.end());
        li.erase(unique(li.begin(), li.end()), li.end());

        n = li.size();
        t = vvi(2 * n);
        for (int i = l; i < r; i++) {
            int j = idx(a[i][1]);
            t[n + j].push_back(a[i][2]);
        }
        for (int i = n - 1; i > 0; --i) {
            merge(t[i<<1], t[i]);
            merge(t[i<<1|1], t[i]);
        }
    }

    vi query(int yl, int yh) {
        int l = idx(yl), r = idx(yh);
        vi res;
        for (l += n, r += n; l < r; l >>= 1, r >>= 1) {
            if (l & 1) merge(t[l++], res);
            if (r & 1) merge(t[--r], res);
        }
        return res;
    }
};

struct segtree2 {
    vector<segtree1> t;
    vii b;
    vi li;
    int n;

    int idx(int x) {
        return lower_bound(li.begin(), li.end(), x) - li.begin();
    }

    void init() {
        int m = a.size();
        sort(a.begin(), a.end());

        for (int i = 0; i < m; i++) li.push_back(a[i][0]);
        li.erase(unique(li.begin(), li.end()), li.end());
        n = li.size();

        b = vii(2 * n, {1e9, -1});
        t = vector<segtree1>(2 * n);
        for (int i = 0; i < m; i++) {
            int j = idx(a[i][0]);
            b[n + j].first = min(b[n + j].first, i);
            b[n + j].second = max(b[n + j].second, i + 1);
        }
        for (int i = 0; i < n; i++) {
            int j = n + i;
            t[n + i].init(b[n + i].first, b[n + i].second);
        }
        for (int i = n - 1; i > 0; --i) {
            b[i].first = min(b[i<<1].first, b[i<<1|1].first);
            b[i].second = max(b[i<<1].second, b[i<<1|1].second);
            t[i].init(b[i].first, b[i].second);
        }
    }

    bool query(int xl, int xh, int yl, int yh) {
        int l = idx(xl), r = idx(xh);
        vi res;
        for (l += n, r += n; l < r; l >>= 1, r >>= 1) {
            if (l & 1) {
                vi tmp = t[l++].query(yl, yh);
                merge(tmp, res);
            }
            if (r & 1) {
                vi tmp = t[--r].query(yl, yh);
                merge(tmp, res);
            }
        }
        if (res.size() >= 100) return true;
        sort(res.begin(), res.end());
        for (int i = 2; i < res.size(); i++) {
            if (res[i - 2] + res[i - 1] > res[i]) return true;
        }
        return false;
    }
};

void solve() {
    int n, q;
    cin >> n >> q;

    a = vvi(n, vi(3));
    for (vi& v : a) {
        for (int& x : v) cin >> x;
    }

    segtree2 st;
    st.init();

    for (int i = 0; i < q; i++) {
        int xl, yl, xh, yh;
        cin >> xl >> yl >> xh >> yh;
        cout << st.query(xl, xh + 1, yl, yh + 1) << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
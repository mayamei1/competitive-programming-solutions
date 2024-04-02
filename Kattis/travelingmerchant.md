---
tags:
  - competitive-programming/catalog/kattis
name: Traveling Merchant
---
#competitive-programming/ds/segment-tree
## _Solution:_
Build segment trees for each potential offset and process the queries that are relevant to that offset. Segment tree keeps track of `min`, `max`, `r_diff` (maximum difference left-to-right direction), `l_diff` (in the right-to-left direction). When "summing" the two halves, take `min` and `max` of both sides, and the `l_diff` is the `max(left.diff, right.diff, left.max - right.min)`

https://open.kattis.com/problems/travelingmerchant
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>
#include <bitset>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll

using namespace std;

struct aa {
    int max, min, l_diff, r_diff;
};

// size 4 * n, root = 1
// vi t(4*n)

// build(vals, 1, 0, n - 1)
void build(vector<aa>& t, vi& vals, int v, int tl, int tr) {
    if (tl == tr) {
        t[v].max = t[v].min = vals[tl];
        t[v].l_diff = t[v].r_diff = 0;
    } else {
        int tm = (tl + tr) / 2;
        build(t, vals, v*2, tl, tm);
        build(t, vals, v*2+1, tm+1, tr);
        t[v].max = max(t[v*2].max, t[v*2+1].max);
        t[v].min = min(t[v*2].min, t[v*2+1].min);
        t[v].l_diff = max(max(t[v*2].l_diff, t[v*2+1].l_diff), t[v*2].max - t[v*2+1].min);
        t[v].r_diff = max(max(t[v*2].r_diff, t[v*2+1].r_diff), t[v*2+1].max - t[v*2].min);
    }
}

// sum(1, 0, n - 1, l, r)
aa sum(vector<aa>& t, int v, int tl, int tr, int l, int r) {
    if (l > r) return {0, 0, -1, -1};
    if (l == tl && r == tr) return t[v];
    int tm = (tl + tr) / 2;
    aa left = sum(t, v*2, tl, tm, l, min(r, tm));
    aa right = sum(t, v*2+1, tm + 1, tr, max(l, tm+1), r);
    if (left.l_diff == -1) return right;
    if (right.l_diff == -1) return left;

    aa ans;
    ans.max = max(left.max, right.max);
    ans.min = min(left.min, right.min);
    ans.l_diff = max(left.l_diff, right.l_diff); ans.l_diff = max(0, ans.l_diff);
    ans.r_diff = max(left.r_diff, right.r_diff); ans.r_diff = max(0, ans.r_diff);
    ans.l_diff = max(ans.l_diff, left.max - right.min);
    ans.r_diff = max(ans.r_diff, right.max - left.min);

    return ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vi v(n);
    vi d(n);
    for (int i = 0; i < n; i++) {
        cin >> v[i] >> d[i];
    }

    int q;
    cin >> q;

    vii queries(q);
    for (int i = 0; i < q; i++) {
        cin >> queries[i].first >> queries[i].second;
        queries[i].first--; queries[i].second--;
    }

    vi vals(n);
    vector<aa> tree(4 * n);
    vi ans(q);
    for (int i = 0; i < 7; i++) {
        for (int j = 0; j < n; j++) {
            vals[j] = v[j];

            int offset = (j - i + 7) % 7;
            if (offset == 1 || offset == 5) vals[j] += d[j];
            else if (offset == 2 || offset == 4) vals[j] += 2 * d[j];
            else if (offset == 3) vals[j] += 3 * d[j];
        }


        build(tree, vals, 1, 0, n - 1);

        for (int j = 0; j < q; j++) {
            int s = queries[j].first;
            int t = queries[j].second;
            if (s < t && (s % 7) == i) {
                ans[j] = sum(tree, 1, 0, n - 1, s, t).r_diff;
            } else if (s > t && ((s + 1) % 7) == i) {
                ans[j] = sum(tree, 1, 0, n - 1, t, s).l_diff;
            }
        }   
    }

    for (int a : ans) {
        cout << a << '\n';
    }
}
```
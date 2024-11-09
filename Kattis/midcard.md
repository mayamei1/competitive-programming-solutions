---
tags:
  - competitive-programming/judges/kattis
name: Mid Card
date: 2024-10-24
---
#competitive-programming/segment-tree #competitive-programming/math/combinatorics 
## _Solution:_
For a particular round, we can use a generating function to describe the ways to win certain amounts. In particular, we can denote round $i$'s function to be $1+(H_{i}-L_{i}+1)x$. Then, if we multiply any two rounds' generating functions together, we the coefficient of $x^{d}$ will give us the ways to win $d$ times. We can extend this to any set of rounds. Then, to process each query of type $0$, we need to multiply all functions between $A$ and $B$. Using a segment tree, we can find the answer in $O(C\log(n))$, where $C$ is the cost for performing the convolution. Note that since we only need to check up to $100$ wins, we can naively do the convolution (however, note that the time limit makes it so that you should avoid doing calculations with any terms with coefficients equal to $0$).

https://open.kattis.com/problems/midcard
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

const int N = 1e5;
int n, c, q;
vi t[2 * N];
int MOD = 1e9 + 7;

void merge(vi& l, vi& r, vi& res) {
    int n = l.size(), m = r.size();
    int k = min(100, n + m - 2);
    res = vi(k + 1);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m && i + j <= 100; j++) {
            res[i + j] += 1ll * l[i] * r[j] % MOD;
            res[i + j] %= MOD;
        }
    }
}

void build() {  // build the tree
    for (int i = n - 1; i > 0; --i) {
        merge(t[i<<1], t[i<<1|1], t[i]);
    }
}

void modify(int p, int value) {  // set value at position p
    for (t[p += n][1] = value; p > 1; p >>= 1) {
        merge(t[p], t[p^1], t[p>>1]);
    }
}

vi res;
void query(int l, int r) {  // sum on interval [l, r)
    res = {1};
    for (l += n, r += n; l < r; l >>= 1, r >>= 1) {
        if (l&1) {
            vi tmp = res;
            merge(tmp, t[l], res);
            l++;
        }
        if (r&1) {
            r--;
            vi tmp = res;
            merge(tmp, t[r], res);
        }
    }
}

void solve() {
    memset(t, 0, sizeof(t));

    cin >> n >> c >> q;
    for (int i = 0; i < n; i++) {
        int a, b;
        cin >> a >> b;
        t[n + i] = {1, b - a + 1};
    }

    build();

    for (int i = 0; i < q; i++) {
        int op;
        cin >> op;
        if (op) {
            int p, a, b;
            cin >> p >> a >> b;
            modify(p - 1, b - a + 1);
        } else {
            int a, b, k;
            cin >> a >> b >> k;
            query(a - 1, b);
            cout << res[k] << endl;
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
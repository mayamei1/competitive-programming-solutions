---
tags:
  - competitive-programming/judges/kattis
name: Genetic Reconstruction
date: 2024-10-09
---
#competitive-programming/complete-search #competitive-programming/greedy #competitive-programming/graph/dag 
## _Solution:_
Try every combination of giving first allele to one parent or second parent. Let's denote lowercase letters to be a known allele, while an uppercase letter to be the most dominant allele it could be. So, initially, for some creature with eye color `x`, their alleles would be `xX`. The graph is a DAG, so we can go bottom-up, and "transfer" the allele up. Say we are transferring allele `a` to a parent with alleles `p1` and `p2`. Let's consider each case:
- `a` is lowercase
	- `p1==a`, the "source" of `a` is `p1`
	- `p1>a`, this contradicts
	- `p1<a`
		- `p2` is lowercase
			- `p2==a`, source of `a` is `p2`
			- `p2!=a`, this contradicts
		- `p2` is uppercase
			- `p2>a`, this contradicts
			- `p2<=a`, set `p2=a` and the source of `a` is `p2`
- `a` is uppercase
	- `p1>=a`, the source of `a` is `p1`
	- `p1<a`
		- `p2` is uppercase
			- `p2>=a`, source of `a` is `p2`
			- `p2<a`, set `p2=max(p2,a)` and the source of `a` is `p2`
Once every source has been set and there were no contradictions, then we can now iterate top-down to "collapse" uppercase letters down. If a creature has no parents, simply make the letter lowercase. If a creature has a parent, then take from the source.

https://open.kattis.com/problems/geneticreconstruction
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

bool update(char a, char p1, char& p2, bool& s) {
    if (a & 32) {
        s = 0;
        if (p1 == a) return true;
        if (p1 > a) return false;
        s = 1;
        if (p2 & 32) return a == p2;
        if ((p2 | 32) > a) return false;
        p2 = a;
        return true;
    } else {
        s = 0;
        char tmp = a | 32;
        if (p1 >= tmp) return true;
        s = 1;
        if (p2 & 32) return tmp <= p2;
        p2 = max(p2, a);
        return true;
    }
}

void solve() {
    int n;
    cin >> n;

    vvi adj(n);
    string base, best;
    best.append(2 * n, 'z');
    for (int i = 0; i < n; i++) {
        int p1, p2;
        char c;
        cin >> p1 >> p2 >> c;
        p1--, p2--;
        base.push_back(c);
        base.push_back(c & ~32);
        adj[i].push_back(p1);
        adj[i].push_back(p2);
    }

    int bm = 1 << n;
    for (int m = 0; m < bm; m++) {
        string cur = base;
        bool fail = false;
        vi source(2 * n);
        for (int i = n - 1; i >= 0; i--) {
            if (adj[i][0] == -1) continue;
            int j = (m >> i) & 1;
            int p1 = adj[i][j], p2 = adj[i][!j];
            
            bool s;
            if (!update(cur[2 * i], cur[2 * p1], cur[2 * p1 + 1], s)) {
                fail = true;
                break;
            }
            source[2 * i] = 2 * p1 + s;
            if (!update(cur[2 * i + 1], cur[2 * p2], cur[2 * p2 + 1], s)) {
                fail = true;
                break;
            }
            source[2 * i + 1] = 2 * p2 + s;
        }
        if (fail) continue;
        for (int i = 0; i < n; i++) {
            char& c = cur[2 * i + 1];
            if (c & 32) continue;
            if (adj[i][0] == -1) {
                c |= 32;
                continue;
            }
            int j = (m >> i) & 1;
            int p2 = adj[i][!j];
            c = cur[source[2 * i + 1]];
        }
        best = min(best, cur);
    }

    if (best[0] == 'z') {
        cout << -1 << endl;
        return;
    }

    for (int i = 0; i < n; i++) {
        cout << best[2 * i] << best[2 * i + 1] << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Vacuum Tubes
date: 2024-11-05
---
#competitive-programming/ds #competitive-programming/binary-search #competitive-programming/greedy 
## _Solution:_
Use a multiset to keep track of all unused elements in sorted order. Then, iterate through every pair $(a_{i},a_{j})$, removing them from the multiset, and after the iteration is finished, putting them back in. For each pair, binary search to find the largest value smaller than $l_{1}-a_{i}$, and remove it from the multiset. Do the same with $l_{2}-a_{j}$. This gives use four tubes. Keep track of the largest sum.

https://open.kattis.com/problems/vacuum
```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;
using dd = int;
using vi = vector<dd>;
using vvi = vector<vi>;
using ii = pair<dd,dd>;
using vii = vector<ii>;
using vvii = vector<vii>;

int main() {
    int l1, l2, n;
    cin >> l1 >> l2 >> n;

    vi a(n);
    for (int& x : a) cin >> x;

    multiset<int> b;
    for (int x : a) b.insert(x);

    int mx = -1;

    for (int i = 0; i < n; i++) {
        int x = a[i];
        if (x >= l1) continue;
        b.erase(b.find(x));
        for (int j = 0; j < n; j++) {
            if (i == j) continue;
            int y = a[j];
            if (y >= l2) continue;
            b.erase(b.find(y));

            auto itr1 = b.upper_bound(l1 - x);
            if (itr1 == b.begin()) {
                b.insert(y);
                continue;
            }
            itr1--;
            int z = *itr1;
            b.erase(itr1);

            auto itr2 = b.upper_bound(l2 - y);
            if (itr2 != b.begin()) {
                itr2--;
                int w = *itr2;
                mx = max(mx, x + y + w + z);
            }
            b.insert(z);
            
            b.insert(y);
        }
        b.insert(x);
    }

    if (mx == -1) cout << "impossible" << endl;
    else cout << mx << endl;
}
```
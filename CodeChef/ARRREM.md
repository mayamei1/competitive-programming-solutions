---
tags:
  - competitive-programming/judges/codechef
name: Array Removal
date: 2024-07-10
---
#competitive-programming/greedy #competitive-programming/sorting 
## _Solution:_
The equivalent problem is, if we look at every first $i$ smallest values ($1\le i\le n$), will the resulting bitwise OR result in $2^x-1$. Then, the answer can be found as $n-i$, where $i$ is the max value where the condition still holds. The reason for this is that if we look for an answer for a particular $x$, then, you would only want to include values that are less than or equal to $2^x-1$. Thus, if you sort the array, then the array can be grouped by their most significant bit. At the end of each group is where each check would take place, but looking at each position does not affect the answer.

https://www.codechef.com/problems/ARRREM
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

const int N = 1e5 + 2;
int a[N];

vvi m;
int query(int l, int r) {
    int len = r - l + 1;
    int k = __lg(len);
    return m[l][k] | m[r-(1<<k)+1][k];
}

void solve() {
    int n;
    cin >> n;

    for (int i = 0; i < n; i++) cin >> a[i];

    sort(a, a + n);

    int ans = -1;
    int val = 0;
    for (int i = 0; i < n; i++) {
        val |= a[i];

        int tmp = val;
        while (tmp & 1) tmp >>= 1;

        if (!tmp) ans = i;
    }

    cout << (n - ans - 1) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
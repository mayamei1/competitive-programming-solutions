---
tags:
  - competitive-programming/judges/codechef
name: Binary Conversion
date: 2024-07-17
---
#competitive-programming/greedy 
## _Solution:_
The trivial check is if $s$ and $t$ do not have the same number of 0's and 1's. From now on, assume they have equal 0's and 1's. Say we have a length $n>2$. We will call $cnt$ the number of mismatches between $s$ and $t$. Then, the number of swaps necessary is $swp=\frac{cnt}{2}$. If there are more swaps that need to be performed, they can be used to swap two of the same element. Thus, as long as $swp\le k$, the answer is yes. Now, for the edge case of $n=2$. If both strings only contain 1's, or only contains 0's, then the answer will always be yes. Otherwise, the parity of $swp$ must be the same as the parity of $k$.

https://www.codechef.com/problems/CONVERT
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

void solve() {
    int n, k;
    cin >> n >> k;
    string s, t;
    cin >> s >> t;

    int cnt = 0;
    int scnt = 0, tcnt = 0;
    for (int i = 0; i < n; i++) {
        if (s[i] != t[i]) cnt++;
        if (s[i] == '0') scnt++;
        if (t[i] == '0') tcnt++;
    }

    if (scnt != tcnt) {
        cout << "NO" << endl;
        return;
    }

    int swp = cnt / 2;
    if (n == 2) {
        if (scnt == 0 && tcnt == 0) cout << "YES" << endl;
        else if (scnt == 2 && tcnt == 2) cout << "YES" << endl;
        else if (swp % 2 == k % 2) cout << "YES" << endl;
        else cout << "NO" << endl;
        return;
    }

    if (swp <= k) cout << "YES" << endl;
    else cout << "NO" << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
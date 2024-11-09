---
tags:
  - competitive-programming/judges/codechef
name: Make Bob Win
date: 2024-07-31
---
#competitive-programming/greedy 
## _Solution:_
For this game, the number of moves necessary for either player is the number of continuous segments of the element that they want to disappear, denoted $a$ and $b$. Say we perform a flip on any index $i$ where $2\le i\le n-1$: the difference in the number of moves does not change. Now, observe that the difference in number of moves necessary by either players will be at most 1. If $a>b$, then obviously no moves are needed. If $a=b$, then the string should have a 1 on one end and a 0 on the other, and using one operation, we can make it 1 on both ends, resulting in $a>b$. If $a<b$, then we must have had 0 on both ends, so using two operations, we make it 1 on both ends, and resulting in $a>b$.

https://www.codechef.com/START145B/problems/DLSB
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

void solve() {
    int n;
    cin >> n;

    string s;
    cin >> s;

    int a = 0, b = 0;
    int p = 0;
    for (int i = 0; i < n; i++) {
        if (s[i] == s[p]) continue;
        if (s[p] == '0') b++;
        else a++;
        p = i;
    }

    if (s[p] == '0') b++;
    else a++;

    int ans = 0;
    if (a > b) ans = 0;
    else if (a == b) ans = 1;
    else if (n == 1) ans = 1;
    else ans = 2;

    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
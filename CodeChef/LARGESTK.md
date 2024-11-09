---
tags:
  - competitive-programming/judges/codechef
name: Largest K
date: 2024-07-24
---
#competitive-programming/greedy #competitive-programming/sorting 
## _Solution:_
For some number of distinct elements $l$, we want to take $l$ numbers with the largest frequency. To do this, find the frequency of each number, then sort the frequencies. Then, for each $l$ take the running sum of the frequencies $s$, and calculate $K=\lfloor{\frac{s}{l}}\rfloor\cdot{l}$.

https://www.codechef.com/problems/LARGESTK
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

    vi freq(n + 1);
    for (int i = 0; i < n; i++) {
        int a;
        cin >> a;
        freq[a]++;
    }

    sort(freq.begin(), freq.end(), greater<int>());

    vi rsum(n + 1);
    rsum[0] = freq[0];
    for (int i = 1; i <= n; i++) rsum[i] = rsum[i - 1] + freq[i];

    int ans = 0;
    for (int i = 0; i <= n; i++) {
        if (freq[i] == 0) break;
        int s = rsum[i];
        int l = i + 1;
        ans = max(ans, s / l * l);
    }

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
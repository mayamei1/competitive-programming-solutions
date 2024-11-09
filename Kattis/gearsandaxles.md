---
tags:
  - competitive-programming/judges/kattis
name: Gears and Axles
date: 2024-10-05
---
#competitive-programming/greedy #competitive-programming/sorting 
## _Solution:_
For any given size, we have a list of compatible gears. It is optimal to pair gears, as any larger groups cancels the effects of the middle gears. You can greedily pair the smallest gear with the largest gear, second smallest with second largest, and so on. Then, to calculate the answer, we sum up every $\log(\frac{b}{a})$ for each pair $(a,b)$ where $a\le b$. 

https://open.kattis.com/problems/gearsandaxles
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = double;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

void solve() {
    int n;
    cin >> n;

    map<int, vi> sp;
    for (int i = 0; i < n; i++) {
        double s, c;
        cin >> s >> c;

        sp[s].push_back(c);
    }

    double ans = 0;
    for (auto &[s, a] : sp) {
        sort(a.begin(), a.end());
        int m = a.size();

        for (int i = 0; i < m / 2; i++) {
            ans += log(a[m - i - 1] / a[i]);
        }
    }

    printf("%.9lf\n", ans);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
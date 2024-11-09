---
tags:
  - competitive-programming/judges/kattis
name: Dishonest Lottery
date: 2024-10-05
---
#competitive-programming/trivial 
## _Solution:_
Take in $50n$ integers, and keep count of each number. Then, iterate through each number and check if it has more than $2n$ occurrences.

https://open.kattis.com/problems/dishonestlottery
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

    vi cnt(51);
    for (int i = 0; i < 50 * n; i++) {
        int x;
        cin >> x;

        cnt[x]++;
    }

    bool flag = false;
    for (int i = 1; i <= 50; i++) {
        if (cnt[i] > 2 * n) {
            cout << i << ' ';
            flag = true;
        }
    }

    if (!flag) cout << -1;
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
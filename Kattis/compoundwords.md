---
tags:
  - competitive-programming/judges/kattis
name: Compound Words
date: 2020-04-04
---
#competitive-programming/complete-search 
## _Solution:_
Iterate through each pair of words and concatenate it, then put it in a set.

https://open.kattis.com/problems/compoundwords
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
    vector<string> a;
    string s;
    while (cin >> s) {
        a.push_back(s);
    }

    int n = a.size();
    set<string> ans;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i == j) continue;
            ans.insert(a[i] + a[j]);
        }
    }

    for (string aa : ans) {
        cout << aa << endl;
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
---
tags:
  - competitive-programming/judges/atcoder
name: Buy a Pen
date: 2024-07-12
---
#competitive-programming/trivial 
## _Solution:_
Print the minimum of the colors that are not $C$.

https://atcoder.jp/contests/abc362/tasks/abc362_a
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
    int r, g, b;
    string c;
    cin >> r >> g >> b >> c;

    if (c == "Blue") cout << min(r, g);
    if (c == "Green") cout << min(r, b);
    if (c == "Red") cout << min(g, b);
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
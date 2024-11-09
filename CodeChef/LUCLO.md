---
tags:
  - competitive-programming/judges/codechef
name: Lucky Clover
date: 2024-07-03
---
#competitive-programming/math #competitive-programming/trivial 
## _Solution:_
$(n-1)\cdot 3+4$

https://www.codechef.com/START141D/problems/LUCLO
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
    int n;
    cin >> n;

    cout << (n - 1) * 3 + 4;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
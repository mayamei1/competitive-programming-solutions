---
tags:
  - competitive-programming/judges/atcoder
name: Insert
date: 2024-07-06
---
#competitive-programming/trivial 
## _Solution:_
Simply insert $X$ after $K$-th element.

https://atcoder.jp/contests/abc361/tasks/abc361_a
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

const int N = 100 + 2;
int a[N];

void solve() {
    int n, k, x;
    cin >> n >> k >> x;

    for (int i = 1; i <= n; i++) cin >> a[i];

    for (int i = 1; i <= k; i++) {
        cout << a[i] << ' ';
    }
    cout << x << ' ';
    for (int i = k + 1; i <= n; i++) {
        cout << a[i] << ' ';
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}

```
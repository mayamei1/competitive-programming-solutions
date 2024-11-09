---
tags:
  - competitive-programming/judges/codechef
name: Chef and Dolls
date: 2024-07-03
---
#competitive-programming/trivial 
## _Solution:_
XOR every value. Alternatively, keep track of the frequency of each number and find the number that only occurs once.

https://www.codechef.com/practice/course/arrays-strings-sorting/INTARR01/problems/MISSP
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

    int ans = 0;
    for (int i = 0; i < n; i++) {
        int a;
        cin >> a;
        ans ^= a;
    }

    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) 
    solve();
}
```
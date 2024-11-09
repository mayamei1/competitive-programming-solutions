---
tags:
  - competitive-programming/judges/codechef
name: Sum of Xors
date: 2024-07-10
---
#competitive-programming/greedy
## _Solution:_
Observe that for some $K$, we can use groups of 4 in a 2-by-2 manner, to effectively cancel to 0, so any $F(K|4)=0$. Then, with a 3-by-3 space, there is a way to use up six 1's to cancel to 0. Thus, if we have enough space to use a 3-by-3, we can fill the rest with the 2-by-2 so that $K=4x+2$, it will also cancel to 0, meaning every even $K$ other than $K=2$ and $K=N\cdot M-2$ can be canceled to 0. If either $N$ or $M$ are 2, then there is not enough space to do the 3-by-3 move, so only $K|4$ can cancel to 0. With any odd numbered $K$, you can always guarantee a value of 2.

https://www.codechef.com/problems/SMXR
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
    ll n, m;
    cin >> n >> m;

    if (n * m == 4) cout << 6 << endl;
    else if (min(n, m) == 2) cout << 3 * (n * m) / 2 << endl;
    else cout << (n * m) + 4 << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
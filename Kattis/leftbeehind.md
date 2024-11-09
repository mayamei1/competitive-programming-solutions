---
tags:
  - competitive-programming/judges/kattis
name: Left Beehind
date: 2019-03-20
---
#competitive-programming/trivial 
## _Solution:_
Check if $x+y=13$: "Never speak again."
Check if $x<y$: "Left beehind."
Check if $x>y$: "To the convention."
Check if $x=y$: "Undecided."

https://open.kattis.com/problems/leftbeehind
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

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int x, y;
    while (cin >> x >> y && !(x == 0 && y == 0)) {
        if (x + y == 13) cout << "Never speak again.\n";
        else if (x < y) cout << "Left beehind.\n";
        else if (x > y) cout << "To the convention.\n";
        else cout << "Undecided.\n";
    }
}
```
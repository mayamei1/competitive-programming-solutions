---
tags:
  - competitive-programming/judges/kattis
name: Cold-puter Science
date: 2019-03-20
---
#competitive-programming/trivial
## _Solution:_
Count numbers less than $0$.

https://open.kattis.com/problems/cold
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

    int n;
    cin >> n;

    int ans = 0;
    for (int i = 0; i < n; i++) {
        int a;
        cin >> a;
        if (a < 0) ans++;
    }
    
    cout << ans;
}
```
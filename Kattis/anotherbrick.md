---
tags:
  - competitive-programming/judges/kattis
name: Another Brick in the Wall
date: 2019-02-11
---
#competitive-programming/simulation 
## _Solution:_
Iterate through each row. With each row, take the next brick until it is greater than or equal to the desired width. If that row is not the desired width, then the answer is `NO`. If all rows are equal to the desired width, then the answer is `YES`.

https://open.kattis.com/problems/anotherbrick
```cpp
#include <bits/stdc++.h>

#define ll long long int
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

    int h, w, n;
    cin >> h >> w >> n;

    vi x(n);
    for (int i = 0; i < n; i++) {
        cin >> x[i];
    }

    int j = 0;
    for (int i = 0; i < h; i++) {
        int width = 0;
        while (j < n && width < w) {
            width += x[j];
            j++;
        }
        if (width != w) {
            cout << "NO\n";
            return 0;
        }
    }

    cout << "YES\n";
}
```
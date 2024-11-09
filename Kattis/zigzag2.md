---
tags:
  - competitive-programming/judges/kattis
name: Zigzag
date: 2024-06-23
---
#competitive-programming/greedy 
## _Solution:_
The maximum subsequence is the same as that of the list of local extrema. The observation can be made that if you included something that goes up, and it is not the local maximum, then the next possible number that you can add has to be after the local maximum, and from there, there can exist a number that is larger than the number you added, but is smaller than the local maximum (by definition). Example `[1,2,4,3]` and you pick `2` (not local max), then you are unable to pick `3`.

https://open.kattis.com/problems/zigzag2
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

const int N = 1e6 + 2;
int a[N];

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    int dir = 0;
    int ans = 1;

    for (int i = 1; i < n; i++) {
        int ndir;
        if (a[i - 1] < a[i]) ndir = 1;
        else if (a[i - 1] > a[i]) ndir = -1;
        else ndir = dir;

        if (ndir == 0) continue;
        if (ndir != dir) ans++;
        dir = ndir;
    }

    cout << ans << endl;
}
```
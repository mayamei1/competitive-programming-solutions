---
tags:
  - competitive-programming/judges/kattis
name: "Hydra's Heads"
date: 2019-03-20
---
#competitive-programming/greedy 
## _Solution:_
You first want to get rid of all of the tails by cutting down two at a time. If there is an odd amount of tails, you need to also spend a move to make it even. Once you cut down all of the tails, if there is an odd amount of heads, then you need to spend three moves (two moves cutting one tail, then one move cutting two tails) to make it even. Then, cut down all of the heads.

https://open.kattis.com/problems/hydrasheads
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

    int h, t;
    while (cin >> h >> t && !(h == 0 && t == 0)) {
        if (t == 0) {
            if (h % 2) cout << "-1" << endl;
            else cout << (h / 2) << endl;
        } else  {
            int moves = (t  + 1) / 2 + (t % 2);
            int t_h = h + (t + 1) / 2;
            if (t_h % 2) {
                moves += 3;
                t_h++;
            }
            moves += t_h / 2;
            cout << moves << endl;
        }
    }
}
```
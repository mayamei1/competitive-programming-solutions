---
tags:
  - competitive-programming/judges/kattis
name: Carnival Generals
date: 2024-05-16
---
#competitive-programming/greedy #competitive-programming/ds #competitive-programming/dp #competitive-programming/permutation 
## _Solution:_
It can be easily proven that there exist a solution for $n=2$. Then, this can be extended to higher $n$ in a bottom-up approach. It can be proven via contradiction that there will always be a way to insert the $n$-th general with a valid $n-1$ permutation.

https://open.kattis.com/problems/carnivalgenerals
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

    list<int> ans;
    ans.push_back(0);
    
    for (int i = 1; i < n; i++) {
        uset<int> allow;
        for (int j = 0; j < i; j++) {
            int p;
            cin >> p;
            if (j <= (i - 1) / 2) allow.insert(p);
        }

        if (allow.find(ans.front()) != allow.end()) {
            ans.push_front(i);
            continue;
        }

        bool fail = true;
        for (auto itr = next(ans.begin()); itr != ans.end(); itr++) {
            if (allow.find(*itr) == allow.end()) continue;
            if (allow.find(*prev(itr)) == allow.end()) continue;
            ans.insert(itr, i);
            fail = false;
            break;
        }

        if (fail) ans.push_back(i);
    }

    for (int a : ans) {
        cout << a << ' ';
    }
}
```
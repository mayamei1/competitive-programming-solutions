---
tags:
  - competitive-programming/judges/kattis
name: Flexible Spaces
date: 2020-02-06
---
#competitive-programming/complete-search
#competitive-programming/trivial
## _Solution:_
Search each pairs of partitions (including $0$ and $w$), and add absolute difference to answer list/set. Do not include $0$ in final answer.

https://open.kattis.com/problems/flexible
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <list>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>
#include <bitset>
#include <iomanip>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll
#define vs vector<string>

#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int w, p;
    cin >> w >> p;
    vi l(p);
    f (i, 0, p) cin >> l[i];
    l.push_back(0);
    l.push_back(w);
    set<int> ans;
    for (int i : l)
        for (int j : l)
            ans.insert(abs(i - j));
    ans.erase(0);
    for (int a : ans) cout << a << ' ';
}
```
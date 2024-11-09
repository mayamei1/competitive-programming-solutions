---
tags:
  - competitive-programming/judges/kattis
name: Contest Advancement
date: 2024-01-29
---
#competitive-programming/greedy 
## _Solution:_
Add team to answer until $s_i$'s count is at $c$, then you instead put them into the extras (keeping the same order). If length of answer is less than $k$, fill with extras.

https://open.kattis.com/problems/contestadvancement
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
#define f(i,s,e) for(ll i = s; i<e; i++)
#define cf(i,s,e) for(ll i=s; i<=e; i++)
#define rf(i,e,s) for(ll i=e-1, i>=s; i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, k, c;
    cin >> n >> k >> c;

    umap<int,int> freq;
    queue<ii> extras;
    int count = 0;
    vi ans(n + 1);
    f (i, 0, n) {
        int t, s;
        cin >> t >> s;

        if (freq.find(s) == freq.end()) freq[s] = 0;
        freq[s]++;
        if (freq[s] > c) {
            extras.push({i, t});
        } else {
            ans[i] = t;
            count++;
            if (count == k) break;
        }
    }

    while (count < k) {
        ii c = extras.front(); extras.pop();
        ans[c.first] = c.second;
        count++;
    }

    f (i, 0, n) {
        if (ans[i]) cout << ans[i] << endl;
    }
}
```
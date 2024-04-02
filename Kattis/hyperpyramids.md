---
tags:
  - competitive-programming/catalog/kattis
name: Pascal's Hyper-Pyramids
---
#competitive-programming/complete-search #competitive-programming/dp #competitive-programming/limit-reduction #competitive-programming/graph/bfs 
## _Solution:_
Instead of representing each location of a hyper-pyramid as its explicit dimensions, you can represent them as the frequency of position values (example: $(1,2,2,3)$ can be represented instead as $(0,1,2,1,0,0,\cdots)$). Then, starting from the base case of $(d, 0, 0, \cdots)=1$, you can BFS through the heights of the hyper-pyramid, and add to every possible new location. For example, $(0,1,2,0,0,\cdots)$ can add to $(0,0,3,0,0,\cdots)$ three times, and $(0,1,1,1,0,0,\cdots)$ once. Do this until you reach the desired height.

https://open.kattis.com/problems/hyperpyramids
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

#define ll long long int
#define ull unsigned ll
#define vs vector<string>
#define dd ll
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

struct hash_vi {
    size_t operator()(const vi &v) const {
        auto hash = v.size();
        for(auto &i : v) {
            hash ^= i + 0x9e3779b9 + (hash << 6) + (hash >> 2);
        }
        return hash;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    ll d, h;
    cin >> d >> h;

    umap<vi, ll, hash_vi> dp, n_dp;
    vi base = vi(h + 1);
    base[1] = d;
    dp[base] = 1;
    f (i, 1, h) {
        n_dp.clear();

        for (auto c : dp) {
            f (j, 1, h) {
                if (!c.first[j]) continue;
                vi next = c.first;
                next[j]--;
                next[j + 1]++;
                if (n_dp.find(next) == n_dp.end()) n_dp[next] = 0;
                n_dp[next] += c.second * next[j + 1];
            }
        }

        swap(dp, n_dp);
    }

    set<ll> ans;
    for (auto c : dp) {
        ans.insert(c.second);
    }

    for (ll a : ans) {
        cout << a << endl;
    }
}
```
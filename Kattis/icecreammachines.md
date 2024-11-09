---
tags:
  - competitive-programming/judges/kattis
name: Ice Cream Machines
date: 2024-04-04
---
#competitive-programming/greedy #competitive-programming/simulation #competitive-programming/binary-search
## _Solution:_
This problem is synonymous to CPU cache replacement policies. The theoretically most optimal policy is [the clairvoyant algorithm](https://en.wikipedia.org/wiki/Cache_replacement_policies#B%C3%A9l%C3%A1dy's_Anomaly_in_Page_Replacement_Algorithms) (this requires knowing the future, which we do). The cache can be implemented as a hash-table. The policy can be implemented through a sorted list of indices for each flavor and binary searching to find the next closest occurrence of a particular page/flavor, and storing the index/flavor pair in a RB-tree. To pick the flavor to replace, select the one with the highest index. Ensure for the list of indices that you also include an `INF` value at the end to indicate that there are no more occurrences. Ensure that when simulating, if the minimum index in the RB-tree is the current one, that you replace it with the next occurrence.

https://open.kattis.com/problems/icecreammachines
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

    int n, m, k;
    cin >> n >> m >> k;
    vi cc(n);
    vvi next(m);
    f (i, 0, n) {
        cin >> cc[i];
        cc[i]--;
        next[cc[i]].push_back(i);
    }

    f (i, 0, m) {
        next[i].push_back(10000000);
    }

    int ans = 0;
    uset<int> cache;
    set<ii> n_occur;
    f (i, 0, n) {
        if (cache.find(cc[i]) == cache.end()) {
            ans++;

            if (cache.size() == k) {
                auto rem = prev(n_occur.end());
                cache.erase(rem->second);
                n_occur.erase(rem);
            }

            int n_i = *lower_bound(next[cc[i]].begin(), next[cc[i]].end(), i + 1);
            cache.insert(cc[i]);
            n_occur.insert({n_i, cc[i]});
        }

        auto ic = n_occur.begin();
        if (ic->first == i) {
            n_occur.erase(ic);
            int n_i = *lower_bound(next[cc[i]].begin(), next[cc[i]].end(), i + 1);
            n_occur.insert({n_i, cc[i]});
        }
    }

    cout << ans;
}
```
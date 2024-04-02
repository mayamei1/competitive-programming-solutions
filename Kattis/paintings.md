---
tags:
  - competitive-programming/catalog/kattis
name: Paintings
---
#competitive-programming/complete-search 
## _Solution:_
Recursive backpropagation. If the next color causes an invalid pairing, skip. Also, keep track of the first valid solution.

https://open.kattis.com/problems/paintings
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

struct hash_pair {
    template <class T1, class T2>
    size_t operator()(const pair<T1, T2>& p) const {
        auto hash1 = hash<T1>{}(p.first);
        auto hash2 = hash<T2>{}(p.second);
        return hash1 ^ (hash2 * (hash1 != hash2));
    }
};

int n, m;
int visited;
int mask_max;
uset<int> path_set;
vi path;
vi fav_path;
uset<ii, hash_pair> invalid;
int ans;

bool solve(bool fav) {
    if (visited == mask_max) {
        ans++;
        if (fav) {
            fav_path = path;
            return true;
        }
        return false;
    }

    f (i, 0, n) {
        if (path_set.find(i) != path_set.end()) continue;
        if (!path.empty() && invalid.find({path.back(), i}) != invalid.end()) continue;

        path.push_back(i);
        path_set.insert(i);
        visited = visited ^ (1 << i);
        if (solve(fav)) fav = false;
        path.pop_back();
        path_set.erase(i);
        visited = visited ^ (1 << i);
    }

    return !fav;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) {
        ans = 0;
        cin >> n;
        mask_max = (1 << n) - 1;
        vs colors(n);
        umap<string, int> inv_colors;
        invalid = uset<ii, hash_pair>();

        f (i, 0, n) {
            cin >> colors[i];
            inv_colors[colors[i]] = i;
        }

        cin >> m;
        f (i, 0, m) {
            string a, b;
            cin >> a >> b;
            invalid.insert({inv_colors[a], inv_colors[b]});
            invalid.insert({inv_colors[b], inv_colors[a]});
        }

        solve(true);

        cout << ans << endl;
        for (int a : fav_path) cout << (colors[a]) << ' ';
        cout << endl;
    }
}
```
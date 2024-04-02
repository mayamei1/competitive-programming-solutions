---
tags:
  - competitive-programming/catalog/kattis
name: Geppetto
---
#competitive-programming/complete-search #competitive-programming/bitmask 
## _Solution:_
Solution 1: Iterate through bitmasks, and check that every invalid pair does not exist.
Solution 2: Backpropagate

https://open.kattis.com/problems/geppetto
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    cin >> n >> m;

    uset<ii, hash_pair> inv; 
    f (i, 0, m) {
        int a, b;
        cin >> a >> b;
        a--; b--;
        inv.insert({a, b});
    }

    int mask_max = 1 << n;
    int ans = 0;
    f (i, 0, mask_max) {
        bool fail = false;
        for (ii a : inv) {
            if ((i & (1 << a.first)) && (i & (1 << a.second))) {
                fail = true;
                break;
            }
        }

        if (!fail) ans++;
    }

    cout << ans;
}
```
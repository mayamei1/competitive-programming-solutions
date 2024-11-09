---
tags:
  - competitive-programming/judges/kattis
name: Class Picture
date: 2024-03-24
---
#competitive-programming/complete-search 
## _Solution:_
Back propagation, and while keeping track of path, use the most recently added to find valid next elements.

https://open.kattis.com/problems/classpicture
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
vi path;
vi visited;
uset<ii, hash_pair> inv;
bool solve() {
    if (path.size() == n) return true;

    f (v, 0, n) {
        if (visited[v]) continue;
        if (path.size() != 0 && inv.find({path.back(), v}) != inv.end()) continue;

        visited[v] = 1;
        path.push_back(v);
        if (solve()) return true;
        visited[v] = 0;
        path.pop_back();
    }

    return false;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n) {
        path.clear();
        inv.clear();
        umap<string, int> id;
        vs r_id(n);
        string s;
        f (i, 0, n) {
            cin >> s;
            r_id[i] = s;
        }

        sort(r_id.begin(), r_id.end());

        f (i, 0, n) {
            id[r_id[i]] = i;
        }

        cin >> m;
        f (i, 0, m) {
            int u, v;
            cin >> s;
            u = id[s];
            cin >> s;
            v = id[s];
            inv.insert({u, v});
            inv.insert({v, u});
        }

        visited = vi(n);
        if (solve()) {
            for (int p : path) {
                cout << r_id[p] << ' ';
            }
            cout << '\n';
        } else {
            cout << "You all need therapy.\n";
        }
    }
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Erratic Ants
date: 2023-07-20
---
#competitive-programming/graph/bfs
#competitive-programming/graph/sssp
## _Solution:_
Create a hash-map of edges while traversing the initial path. Then BFS to find shortest path to the end.

https://open.kattis.com/problems/erraticants
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>
#include <bitset>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll

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

    int n;
    cin >> n;

    for (int i = 0; i < n; i++) {
        int s;
        cin >> s;

        string d;
        int x = 0, y = 0;
        unordered_map<ii, unordered_set<ii, hash_pair>, hash_pair> adj;

        for (int i = 0; i < s; i++) {
            cin >> d;

            if (d == "N") {
                adj[{x, y}].insert({x, y + 1});
                adj[{x, y + 1}].insert({x, y});
                y++;
            }
            else if (d == "S") {
                adj[{x, y}].insert({x, y - 1});
                adj[{x, y - 1}].insert({x, y});
                y--;
            }
            else if (d == "E") {
                adj[{x, y}].insert({x + 1, y});
                adj[{x + 1, y}].insert({x, y});
                x++;
            }
            else {
                adj[{x, y}].insert({x - 1, y});
                adj[{x - 1, y}].insert({x, y});
                x--;
            }
        }

        queue<pair<ii, int>> q;
        q.push({{0, 0}, 0});
        unordered_set<ii, hash_pair> visited;
        while (!q.empty()) {
            ii c = q.front().first; int d = q.front().second; q.pop();

            if (visited.find(c) != visited.end()) continue;

            visited.insert(c);

            if (c.first == x && c.second == y) {
                cout << d << '\n';
                break;
            }

            for (ii n : adj[c]) {
                q.push({n, d + 1});
            }
        }
    }
}
```
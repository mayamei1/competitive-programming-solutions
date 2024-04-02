---
tags:
  - competitive-programming/catalog/kattis
name: Supply Routes
---
#competitive-programming/ds/disjoint-set
#competitive-programming/work-backwards
#competitive-programming/graph
## _Solution:_
Start by overrunning every street and creating a disjoint set of connected junctions. Iterate through queries backwards: merge if the operation is `0`, find if the operation is `1`

https://open.kattis.com/problems/supplyroutes
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

/*
    Disjoint sets based off index, if a node does not have a parent, then disjoint_set[node] == -1
*/

// create a new forest of trees vi(n, -1)

// find root (representative of group) of n
int find(vi &forest, int n) {
    // get root of n
    int root = n;
    while (forest[root] != -1) {
        root = forest[root];
    }

    // set every node in branch to have root as parent
    int idx = n;
    while (forest[idx] != -1) {
        int parent = forest[idx];
        forest[idx] = root;
        idx = parent;
    }

    return root;
}

// merge two trees/sets
void merge(vi& forest, int n, int m) {
    int r1 = find(forest, n);
    int r2 = find(forest, m);

    if (r1 != r2) {
        forest[r1] = r2;
    }
}

struct query {
    int t, u, v;
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m, q;
    cin >> n >> m >> q;

    vector<unordered_set<int>> adj(n);    
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].insert(v);
        adj[v].insert(u);
    }

    vector<query> queries(q);
    for (int i = 0; i < q; i++) {
        cin >> queries[i].t >> queries[i].u >> queries[i].v;
        if (queries[i].t == 0) {
            adj[queries[i].u].erase(queries[i].v);
            adj[queries[i].v].erase(queries[i].u);
        }
    }

    vi forest(n, -1);
    vector<bool> visited(n);
    for (int i = 0; i < n; i++) {
        if (visited[i]) continue;

        queue<int> q;
        q.push(i);
        visited[i] = true;

        while (!q.empty()) {
            int curr = q.front();
            q.pop();

            for (int next : adj[curr]) {
                if (!visited[next]) {
                    q.push(next);
                    visited[next] = true;
                    merge(forest, curr, next);
                }
            }
        }
    }

    stack<bool> ans;
    for (int i = q - 1; i >= 0; i--) {
        if (queries[i].t) {
            if (find(forest, queries[i].u) == find(forest, queries[i].v)) ans.push(true);
            else ans.push(false);
        } else {
            merge(forest, queries[i].u, queries[i].v);
        }
    }

    while (!ans.empty()) {
        if (ans.top()) cout << "safe\n";
        else cout << "unsafe\n";
        ans.pop();
    }
}
```
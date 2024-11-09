---
tags:
  - competitive-programming/judges/kattis
name: Travelling Caterpillar
date: 2023-04-05
---
#competitive-programming/graph/tree
## _Solution:_
Mark every visited node for all paths from desired nodes to root, then add up every distance/edge between visited nodes.

https://open.kattis.com/problems/travellingcaterpillar
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
#include <map>
#include <set>
#include <limits>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>

using namespace std;

int main() {
    int n,k;
    cin >> n >> k;

    vii root(n);
    for (int i = 0; i < n - 1; i++) {
        int s, t, d;
        cin >> s >> t >> d;
        root[t] = make_pair(s, d);
    }

    vi visited(n);
    for (int i = 0; i < k; i++) {
        int leaf;
        cin >> leaf;

        while (leaf != 0 && !visited[leaf]) {
            visited[leaf] = 1;
            leaf = root[leaf].first;
        }
    }

    int sum = 0;
    for (int i = 1; i < n; i++) {
        if (visited[i]) sum += root[i].second;
    }

    cout << sum * 2;
}
```
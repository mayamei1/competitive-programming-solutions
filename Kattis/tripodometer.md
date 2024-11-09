---
tags:
  - competitive-programming/judges/kattis
name: Trip Odometer
date: 2023-04-05
---
#competitive-programming/ds
#competitive-programming/trivial
## _Solution:_
Sum up all distances, iterate through each distance, and add `sum-dist[i]` to a set.

https://open.kattis.com/problems/tripodometer
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
    int n;
    cin >> n;

    vi d(n);
    int sum = 0;
    for (int i = 0; i < n; i++) {
        cin >> d[i];
        sum += d[i];
    }

    set<int> unique;
    for (int i = 0; i < n; i++) {
        unique.insert(sum - d[i]);
    }

    cout << unique.size() << '\n';
    for (int i : unique) {
        cout << i << ' ';
    }
}
```
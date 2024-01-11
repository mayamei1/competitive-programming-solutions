---
type:
  - competitive-programming
  - kattis
tags:
  - string
  - math
  - ad-hoc
name: Double Password
---
## _Solution:_
Find number of different digits at each location, and the solution is 2 to the power of the number of differences.

https://open.kattis.com/problems/doublepassword
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

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    string p1, p2;
    cin >> p1 >> p2;

    cout << (1 << ((p1[0] != p2[0]) + (p1[1] != p2[1]) + (p1[2] != p2[2]) + (p1[3] != p2[3])));
}
```
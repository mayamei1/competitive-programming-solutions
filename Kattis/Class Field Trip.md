---
type:
  - competitive-programming
  - kattis
tags:
  - string
  - sorting
  - trivial
---
#kattis #kattis-classfieldtrip

## _Solution:_
Combine strings, and sort by character

https://open.kattis.com/problems/classfieldtrip
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    string a, b;
    cin >> a >> b;
    string c = a + b;
    sort(c.begin(), c.end());

    cout << c;
}
```
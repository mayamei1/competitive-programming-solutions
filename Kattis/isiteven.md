---
tags:
  - competitive-programming/judges/kattis
name: Is It Even?
date: 2023-04-05
---
#competitive-programming/math
#competitive-programming/trivial
## _Solution:_
Find out how many times you can divide $n$ by 2.

https://open.kattis.com/problems/isiteven
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
    int n, k;
    cin >> n >> k;

    int sum = 0;
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;

        while (x % 2 == 0) {
            sum++;
            x /= 2;
        }
    }

    cout << (sum >= k);
}
```
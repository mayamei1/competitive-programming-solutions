---
tags:
  - competitive-programming/judges/kattis
name: Magical Runes
date: 2023-04-05
---
#competitive-programming/string
#competitive-programming/math
## _Solution:_
This follows the same behavior as incrementing binary digits

https://open.kattis.com/problems/magicalrunes
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
    string s;
    int d;

    cin >> s >> d;

    int value = 0;
    int idx;
    int digit = 1;
    for (idx = 0; s[idx]; idx++) {
        if (s[idx] == 'B') value += digit;
        digit <<= 1;
    }

    value += d;

    for (int i = 0; i < idx; i++) {
        if (value % 2) cout << 'B';
        else cout << 'A';
        value /= 2;
    }
}
```
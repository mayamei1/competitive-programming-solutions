---
type:
  - competitive-programming
  - kattis
tags:
  - dp
  - work-backwards
  - sorting
---
#kattis #kattis-beastbullies

## _Solution:_
Add animals in descending power, while keeping track of "attacking" and "defending" animals. First animal is the first attacker, and the next animals are put into defending. If power of defending is >= power of attacking, then the defending animals become attacking animals as well.

https://open.kattis.com/problems/beastbullies
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

bool comp(int a, int b) {
    return a > b;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vi p(n);
    for (int i = 0; i < n; i++) {
        cin >> p[i];
    }

    sort(p.begin(), p.end(), comp);

    int m_safe_i = 0;
    ull atk_p = p[0];
    ull def_p = 0;
    for (int i = 1; i < n; i++) {
        def_p += p[i];

        if (def_p >= atk_p) {
            m_safe_i = i;
            atk_p += def_p;
            def_p = 0;
        }
    }

    cout << m_safe_i + 1;
}
```
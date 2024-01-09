---
type:
  - competitive-programming
  - kattis
tags:
  - simulation
---
#kattis #kattis-ghostleg

## _Solution:_
Iterate through each rung and simulate each number

https://open.kattis.com/problems/ghostleg
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

    int n, m;
    cin >> n >> m;

    vi curr_v(n);
    for (int i = 0; i < n; i++) {
        curr_v[i] = i;
    }

    int a;
    for (int i = 0; i < m; i++) {
        cin >> a;
        a--;
        for (int j = 0; j < n; j++) {
            if (curr_v[j] == a) {
                curr_v[j] = a + 1;
            } else if (curr_v[j] == (a + 1)) {
                curr_v[j] = a;
            }
        }
    }

    vi ans(n);
    for (int i = 0; i < n; i++) {
        ans[curr_v[i]] = i + 1;
    }

    for (int i = 0; i < n; i++) {
        cout << ans[i] << '\n';
    }
}
```
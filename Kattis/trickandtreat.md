---
tags:
  - competitive-programming/catalog/kattis
name: Trick and Treat
---
#competitive-programming/simulation
#competitive-programming/complete-search
#competitive-programming/limit-reduction
## _Solution:_
Observation: maximum search space is searching between `[M-10, M]`. If you have any less candy, then you start losing more groups than you gain.

Iterate through `[M-10, M]` and simulate through each group, print out minimum groups that TP.

https://open.kattis.com/problems/trickandtreat
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
    
    vi ms(11);
    vi ans(11);
    for (int i = 0; i <= 10; i++) {
        ms[i] = m - i;
    }

    for (int i = 0; i < n; i++) {
        int a;
        cin >> a;
        for (int j = 0; j <= 10; j++) {
            if (ms[j] >= a) ms[j] -= a;
            else ans[j]++;
        }
    }

    cout << *min_element(ans.begin(), ans.end());
}
```
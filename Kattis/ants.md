---
tags:
  - competitive-programming/catalog/kattis
name: Ants
---
#competitive-programming/simulation
#competitive-programming/problem-reduction
## _Solution:_
Ants bumping into each other is the same as them passing through each other. Calculate maximum time taken for cases of if ants go the more optimal side and if ants go the less optimal side.

https://open.kattis.com/problems/ants
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <list>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>
#include <bitset>
#include <iomanip>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll
#define vs vector<string>

#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int tc;
    cin >> tc;

    while (tc--) {
        int l, n;
        cin >> l >> n;

        int t_mi = 0, t_ma = 0;
        f (i, 0, n) {
            int a;
            cin >> a;
            t_mi = max(t_mi, min(a, l - a));
            t_ma = max(t_ma, max(a, l - a));
        }
        cout << t_mi << ' ' << t_ma << '\n';
    }
}
```
---
type:
  - competitive-programming
tags:
  - ad-hoc
  - simulation
---
#kattis #kattis-maximumfix

## _Solution:_
Grab each number, and determine the minimum rotation necessary for it to be a fixed number. Count up the frequency of each number, and print out the rotation with the maximum frequency (and the count).

https://open.kattis.com/problems/maximumfix
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

    int n;
    cin >> n;

    vi cnt(n);
    f (i, 0, n) {
        int a;
        cin >> a; a--;
        cnt[(i - a + n) % n]++;
    }

    int ans = cnt[0], idx = 0;
    f (i, 1, n) {
        if (cnt[i] > ans) {
            ans = cnt[i];
            idx = i;
        }
    }

    cout << idx << ' ' << ans;
}
```
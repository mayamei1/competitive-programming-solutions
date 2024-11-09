---
tags:
  - competitive-programming/judges/ieeextreme
name: Maximum Sum
date: 2023-10-01
---
#competitive-programming/greedy
#competitive-programming/work-backwards
## _Solution:_
To find any solution with the maximum sum is trivial. Start with a list (or deque) with only the largest value. Then alternate adding the next largest to the left or right of the list until exhausted. However, finding the smallest alphabetical order is harder. In order to find it, work backwards. Start by adding all zeros to the left side. Then start alternating left and right, until a third duplicate shows up (aka the last elements of left and right should be equal to the current), as you will need to add all of the duplicates over two to the left. Once done, return adding to the left, then right, alternating again until the next third duplicate.

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

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

#define LSOne(S) ((S) & -(S))

int t, n;
vi a;
void solve() {
    sort(a.begin(), a.end());

    vi left, right;

    f (i, 0, n) {
        if (a[i] == 0) {
            left.push_back(0);
            continue;
        }

        bool dir;
        if (left.size() == 0) dir = true;
        else if (left.back() == 0) dir = true;
        else if (right.size() == 0) dir = false;
        else dir = left.back() <= right.back();

        if (dir) {
            left.push_back(a[i]);
        } else {
            right.push_back(a[i]);
        }
    }

    a = vi();
    f (i, 0, left.size()) a.push_back(left[i]);
    rf (i, right.size(), 0) a.push_back(right[i]);

    ll sum = 0;
    f (i, 1, n) sum += a[i] * (ll) a[i - 1];
    cout << sum << '\n';

    f (i, 0, n) cout << a[i] << ' ';
    cout << '\n';
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> t;
    while (t--) {
        cin >> n;
        a = vi(n);
        f (i, 0, n) {
            cin >> a[i];
        }
        solve();
    }
}
```
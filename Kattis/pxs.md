---
tags:
  - competitive-programming/catalog/kattis
name: Primary X-Subfactor Series
---
#competitive-programming/complete-search
#competitive-programming/bitmask
#competitive-programming/graph/dag
#competitive-programming/dp
## _Solution:_
Recursively find the next integer in the series by iterating through every subsequence of the current value (using a bitmask) and checking if it is a subfactor. If it is, then recursively find the next integer with that subfactor. While doing so, keep track of the current path, and keep checking if the current path is better than the current "best" path. Optimizations could be done with the observation that this is a DAG and DP can be used to remove some calculations. However, a complete search is fast enough, due to the small input size.

https://open.kattis.com/problems/pxs
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

int len(int a) {
    int count = 0;
    while (a) {
        a /= 10;
        count++;
    }
    return count;
}

bool better(vi& curr, vi& best) {
    if (curr.size() > best.size()) return true;
    if (curr.size() < best.size()) return false;

    for (int i = 0; i < curr.size(); i++) {
        if (curr[i] < best[i]) return true;
        if (curr[i] > best[i]) return false;
    }

    return false;
}

void search(int n, vi& curr, vi& best) {
    curr.push_back(n);

    if (better(curr, best)) best = curr;

    int l = len(n);
    int pow_l = 1 << l;

    for (int i = 1; i < pow_l; i++) {
        int sub = 0, rem = 0;

        int mask = i;
        int pow_sub = 1, pow_rem = 1;
        int temp = n;

        int lead_digit = 0;
        for (int j = 0; j < l; j++) {
            if (mask & 1) {
                lead_digit = temp % 10;
                sub += pow_sub * (temp % 10);
                pow_sub *= 10;
            } else {
                rem += pow_rem * (temp % 10);
                pow_rem *= 10;
            }

            temp /= 10;
            mask >>= 1;
        }

        if (lead_digit != 0 && sub != 0 && sub != 1 && sub != n && (n % sub) == 0) {
            search(rem, curr, best);
        }
    }

    curr.erase(prev(curr.end()));
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    while (cin >> n && n) {
        vi curr, best;
        search(n, curr, best);

        for (int i = 0; i < best.size(); i++) {
            cout << best[i] << ' ';
        }
        cout << '\n';
    }
}
```
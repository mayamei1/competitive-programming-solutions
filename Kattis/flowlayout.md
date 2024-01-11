---
type:
  - competitive-programming
  - kattis
tags:
  - simulation
  - geometry
  - trivial
name: Flow Layout
---
## _Solution:_
Simulate adding rectangles, print minimum width/height of bounding box.

https://open.kattis.com/problems/flowlayout
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

    int m;
    while (cin >> m && m) {
        int ans_w = 0, ans_h = 0;
        int curr_w = 0, curr_h = 0;

        int w, h;
        while (cin >> w >> h && w != -1) {
            if (curr_w + w > m) {
                ans_h += curr_h;
                curr_w = w;
                ans_w = max(ans_w, curr_w);
                curr_h = h;
            } else {
                curr_w += w;
                ans_w = max(ans_w, curr_w);
                curr_h = max(curr_h, h);
            }
        }
        ans_h += curr_h;

        cout << ans_w << " x " << ans_h << '\n';
    }
}
```
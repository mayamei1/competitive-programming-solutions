---
tags:
  - competitive-programming/catalog/kattis
name: Biggest Slice
---
#competitive-programming/simulation
#competitive-programming/limit-reduction
## _Solution:_
Have a bit set of size $360\times60\times60$ or $1296000$. This number is the maximum number of cuts you could make, and is small enough of a number to simulate the cuts. Start at degree $0$ and, as you make cuts, set the corresponding bit in the bit set to $1$. If at any point you come across a $1$ bit, then you can stop early, as the rest of the cuts will be redundant. Iterate through the bit set to find the maximum distance between $1$ bits. Use this distance to calculate the area of the slice.

https://open.kattis.com/problems/biggest
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

using namespace std;

#define LSOne(S) ((S) & -(S))

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    bitset<1296001> bs;

    int m;
    cin >> m;

    int r, n, a, b, c, d;
    for (int i = 0; i < m; i++) {
        bs.reset();
        bs[1296000] = 1;

        cin >> r >> n >> a >> b >> c;
        int d = 3600 * a + 60 * b + c;
        int curr = 0;
        while (!bs[curr] && n) {
            bs[curr] = 1;
            curr = (curr + d) % 1296000;
            n--;
        }

        int prev = 0, ans = 0;
        for (int i = 1; i <= 1296000; i++) {
            if (bs[i]) {
                ans = max(ans, i - prev);
                prev = i;
            }
        }

        cout << fixed << setprecision(6) << M_PI * r * r * ans / 1296000.0 << '\n';
    }
}
```
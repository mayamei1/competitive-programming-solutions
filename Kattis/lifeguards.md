---
tags:
  - competitive-programming/judges/kattis
name: Lifeguards
date: 2023-09-25
---
#competitive-programming/geometry
#competitive-programming/math
#competitive-programming/sorting
## _Solution:_
Sort points by location (e.g. increasing $x$, then decreasing $y$). Find middle point accounting for even/odd parity. Then set the two lifeguards as far away as possible in the $x$ direction, on the same $y$ as the middle. Then if even parity, move one lifeguard up and the other down (based on how you sort points). If odd parity, move one up or down one (depending on sorting again).

The idea is that you can find the "middle point" or the point where you if you have a very slightly slanted vertical that goes through the middle point, it splits the other points evenly. That vertical line slanted so that at any point it doesn't reach the next integer position within $10^{9}$, but any point above the middle point is part of one group, and any point lower than the middle point are part of the other. The vertical line is easily achieved by setting the lifeguards on the same horizontal line, and since we want the middle point to be the mid point of the slant, we set the horizontal line to be on the middle point. If we set the $x$ coordinates of the lifeguards to be outside of the viable points ($>10^{9}$) and evenly spaced from the middle point, then setting the slant is just changing the lifeguard(s) $y$ to $\pm1$, and it will guarantee that at no point, the line doesn't cross over $x\pm1$ of the middle point. Based on even or odd parity, you need to have the middle point be on the line or not. If even, then you change one of the lifeguard's location by one to move the line up or down a bit, so the middle point is no longer on the line. If odd, move one lifeguard by $\pm1$ and the other by $\mp1$. The direction you move the lifeguards depend on how you initially sort the points.

https://open.kattis.com/problems/lifeguards
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
#define e18 1000000000000000000ll

bool comp(const pair<ll, ll>& a, const pair<ll, ll>& b) {
    if (a.first == b.first) return a.second > b.second;
    return a.first < b.first;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<pair<ll, ll>> p(n);
    f (i, 0, n) {
        cin >> p[i].first >> p[i].second;
    }

    sort(p.begin(), p.end(), comp);

    int i = (n - 1) / 2;

    ll mid_x =  p[i].first, mid_y = p[i].second;

    ll x1, y1, x2, y2;
    if (mid_x >= 0) {
        x2 = e18;
        x1 = 2 * mid_x - x2;
    } else {
        x1 = -e18;
        x2 = 2 * mid_x - x1;
    }
    y1 = mid_y + (n % 2);
    y2 = mid_y - 1;

    cout << x1 << ' ' << y1 << '\n';
    cout << x2 << ' ' << y2 << '\n';
}
```
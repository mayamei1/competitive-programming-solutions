---
tags:
  - competitive-programming/judges/kattis
name: Blueberry Waffle
date: 2024-02-19
---
#competitive-programming/math #competitive-programming/trivial 
## _Solution:_
The degree repeats every $2r$ and is flipped down if $\frac{r}{2}\leq f\mod{2r}\leq r + \frac{r}{2}$. Special case is with $r=1$.

https://open.kattis.com/problems/blueberrywaffle
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

    int r, f;
    cin >> r >> f;

    if (r == 1) {
        if (f % 2) cout << "down";
        else cout << "up";
        return 0;
    }

    int a = f % (2 * r);
    int b = r / 2;
    if (b <= a && a <= (b + r)) cout << "down";
    else cout << "up";
    // 0 1 2 3 4|5 6 7 8 9/10 11 12 13 14|15 16 17 18 19
    // 0 1 2 3 | 5 6 7 8 | 10 11 12 13|14 15 16 17
}
```
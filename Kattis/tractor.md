---
type:
  - competitive-programming
  - kattis
tags:
  - problem-reduction
  - math
name: Tractor
---
## _Solution:_
Imagine no bounds for $A$ and $B$. Starting with $n=0$ moves, you start with a "diagonal line" of visited locations with sides of length $1$. With exactly $n=1$ moves, all locations will be new locations, forming a larger "diagonal." This is due to the fact that all moves up to $n$ have to be done in either the $x$ or $y$ direction and cannot be discarded (another way to look at it is that $x\oplus y=2^{n+1}-1$). As you grow $n$,  the amount of new locations you've added are $2^n$.

Now let's add back the bounds of $A$ and $B$. When you grow the diagonal large enough, parts of the it goes over the bounds. "Cutting off" the part of the diagonal where the $x$ greater than $A$ takes out $2^n-A-1$ from the diagonal. Cutting the part where the diagonal's $y$ greater than $B$ takes out $2^n-B-1$. When the sum of what you've cut off is greater than or equal to the amount that you've added ($2^n$), then this and all other diagonals are too large for the bound, and no longer need to be checked.

https://open.kattis.com/problems/tractor
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

ll n, a, b;
ll solve() {
    int p = 0;
    ll ans = 0;

    while (true) {
        ll curr = 1ll << p;
        ll cutx = max(0ll, curr - a - 1);
        ll cuty = max(0ll, curr - b - 1);
        if (curr <= (cutx + cuty)) break;
        ans += curr - cutx - cuty;
        p++;
    }

    return ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;
    while (n--) {
        cin >> a >> b;
        cout << solve() << endl;
    }
}
```
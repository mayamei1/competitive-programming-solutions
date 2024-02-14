---
type:
  - competitive-programming
  - kattis
tags:
  - math/gcd
name: Jackpot
---
## _Solution:_
Find the LCM of every periodicity per machine. If LCM at any point goes over a billion, keep a boolean flag to keep track.

https://open.kattis.com/problems/jackpot
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

ll gcd(ll a, ll b) {
    if(a == 0) return b;
    return gcd(b % a, a);
}

ll lcm(ll a, ll b) {
    return a / gcd(a, b) * b;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    while (n--) {
        int w;
        cin >> w;

        ll sol, next;
        cin >> sol;
        bool over = false;
        f (i, 1, w) {
            cin >> next;
            sol = lcm(sol, next);
            if (sol > 1000000000ll) over = true;
        }

        if (over) cout << "More than a billion.\n";
        else cout << sol << '\n';
    }
}
```
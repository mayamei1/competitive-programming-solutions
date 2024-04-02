---
tags:
  - competitive-programming/catalog/kattis
name: Ternarian Weights
---
#competitive-programming/math
## _Solution:_
Calculate the ternary representation of $x$. As you get the next digit, do the following. If digit is $1$, add that power to the right pan. If the digit is $2$, add that power to the left, and add to $x$. If the digit is $0$, don't do anything extra.

https://open.kattis.com/problems/ternarianweights
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

int n, x;
void solve() {
    vi l, r;

    int pow = 1;
    while (x) {
        int carry = 0;
        if (x % 3 == 1) {
            r.push_back(pow);
        } else if (x % 3 == 2) {
            l.push_back(pow);
            carry = 1;
        }

        pow *= 3;
        x /= 3;
        x += carry;
    }

    reverse(l.begin(), l.end());
    reverse(r.begin(), r.end());

    cout << "left pan:";
    for (int i : l) cout << " " << i;
    cout << '\n';

    cout << "right pan:";
    for (int i : r) cout << " " << i;
    cout << '\n';
    cout << '\n';
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;
    while (n--) {
        cin >> x;
        solve();
    }
}
```
---
tags:
  - competitive-programming/judges/kattis
name: Salt
date: 2024-05-24
---
#competitive-programming/greedy 
## _Solution:_
The problem asks for to convert $a$ to $n$ consecutive numbers and guarantees a solution. The XOR operation in a bitwise level does the following: $1$ flips the current bit, and $0$ keeps the current bit. Because of this property, we can do the following. Look at the most significant bit of every $a_i$. If they are in non-decreasing order, then it must mean that the bit has not been flipped, and the MSB of $s$ must be 0. Otherwise, it must be $1$ (since the problem guarantees a solution). Then, look at the two most significant bits of every $a_i$ and check if they are in non-decreasing order. If they are, then the second most significant bit of $s$ must be $0$. Keep doing this up to the least significant bit and we get $s$.

https://codesprintla24.kattis.com/contests/codesprintla24open/problems/salt
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

#define ll long long int
#define ull unsigned ll
#define vs vector<string>
#define dd ll
#define ii pair<dd, dd>
#define vi vector<dd>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define umap unordered_map
#define uset unordered_set

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vi a(n);
    ll mx = 0;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
        mx = max(mx, a[i]);
    }

    ll s = 0;
    int m = __lg(mx);
    for (int i = m; i >= 0; i--) {
        int flip = 0;
        for (int j = 1; j < n; j++) {
            int x = (a[j - 1] ^ s) >> i;
            int y = (a[j] ^ s) >> i;
            if (x > y) {
                flip = 1;
                break;
            }
        }
        s |= flip << i;
    }

    cout << s << endl;
}
```
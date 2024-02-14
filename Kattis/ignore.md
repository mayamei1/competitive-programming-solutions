---
type:
  - competitive-programming
  - kattis
tags:
  - math/combinatorics
name: Ignore the Garbage
---
## _Solution:_
Only 7 acceptable digits. Map the 7 digits in ascending order to the parities of $\mod 7$. Then, get every digit of $n$ in base 7, and map it to the the acceptable digits (rotated 180).

https://open.kattis.com/problems/ignore
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

    ll k;
    while (cin >> k) {
        ll tmp = k;
        string ans;
        while (tmp) {
            int digit = tmp % 7;
            if (digit == 0) ans += "0";
            else if (digit == 1) ans += "1";
            else if (digit == 2) ans += "2";
            else if (digit == 3) ans += "5";
            else if (digit == 4) ans += "9";
            else if (digit == 5) ans += "8";
            else if (digit == 6) ans += "6";
            tmp /= 7;
        }
        cout << ans << endl;
    }
}
```
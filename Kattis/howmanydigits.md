---
tags:
  - competitive-programming/judges/kattis
name: How Many Digits?
date: 2024-04-01
---
#competitive-programming/math/factorials #competitive-programming/math/log-trick
## _Solution:_
Instead of dealing with big integers, since we are already looking for number of digits, we can do our calculations in $\log_{10}(n!)$. The log factorials can be calculated with the recursive function
$$
\log_{10}n!=\log_{10}n+\log_{10}(n-1)!
$$
With the base case $log_{10}0!=0$. Proof:
$$
\begin{align*}
\log_{10}n!&=\log_{10}(1\times2\times\cdots\times n)\\
&=\log_{10}1+\log_{10}2+\cdots+\log_{10}n\\
&=\log_{10}(n-1)!+\log_{10}n
\end{align*}
$$

https://open.kattis.com/problems/howmanydigits
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
#define dd double
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

    vi ans(1000001);
    ans[0] = 0;
    cf (i, 1, 1000000) {
        ans[i] = log10(i) + ans[i - 1];
    }
    ll n;

    while (cin >> n) {
        cout << (int)ans[n] + 1 << endl;
    }
}
```
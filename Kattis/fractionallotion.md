---
tags:
  - competitive-programming/judges/kattis
name: Fractional Lotion
date: 2024-04-08
---
#competitive-programming/complete-search #competitive-programming/limit-reduction #competitive-programming/math 
## _Solution:_
You only need to search $n<x\leq2n$, and you can calculate $\frac{1}{n}- \frac{1}{x}$ and check if the simplified numerator is $1$ (aka if denominator is divisible by numerator). This problem is a tight fit, if needed for slower languages, you can cache solutions for $n$.

https://open.kattis.com/problems/fractionallotion
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
#define dd int
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

int gcd(int a, int b) {
    if(a == 0) return b;
    return gcd(b % a, a);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    
    char c;
    string s;
    while (cin >> c) {
        cin >> c;
        int n;
        cin >> n;
        getline(cin, s);
        
        int ans = 0;
        f (x, n + 1, 2 * n + 1)
            if ((x * n) % (x - n) == 0) ans++;
        cout << ans << endl;
    }
}
```
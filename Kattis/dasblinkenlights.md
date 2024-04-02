---
tags:
  - competitive-programming/catalog/kattis
name: Das Blinkenlights
---
#competitive-programming/math/gcd
## _Solution:_
Check if the LCM of $p$ and $q$ is at most $s$.

https://open.kattis.com/problems/dasblinkenlights
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

int gcd(int a, int b) {
    if(a == 0) return b;
    return gcd(b % a, a);
}

int lcm(int a, int b) {
    return a * b / gcd(a, b);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int p, q, s;
    cin >> p >> q >> s;

    if (lcm(p, q) <= s) cout << "yes";
    else cout << "no";
}
```
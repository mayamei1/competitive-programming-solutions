---
tags:
  - competitive-programming/judges/kattis
name: Saving For Retirement
date: 2020-04-01
---
#competitive-programming/math
#competitive-programming/trivial
## _Solution:_
Calculate Bob's retirement savings, and calculate the number of years necessary for Alice to save to go over that. Add that to Alice's current age. Bob's total is $B_t=(B_r-B)\times B_s$, and Alice needs to save for $\lfloor{\frac{B_t}{A_s}}\rfloor+1$ years.

https://open.kattis.com/problems/savingforretirement
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

    int b, br, bs, a, as;
    cin >> b >> br >> bs >> a >> as;


    int bob = (br - b) * bs;
    cout << bob / as + 1 + a;
}
```
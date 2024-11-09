---
tags:
  - competitive-programming/judges/kattis
name: Water Journal
date: 2024-01-29
---
#competitive-programming/trivial
#competitive-programming/math
## _Solution:_
Check if the maximum and minimum numbers have appeared previously. If only one is missing, then it is the other. If both are missing, its impossible. If both are present, it can be any number between the range.

https://open.kattis.com/problems/waterjournal
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
#define f(i,s,e) for(ll i = s; i<e; i++)
#define cf(i,s,e) for(ll i=s; i<=e; i++)
#define rf(i,e,s) for(ll i=e-1, i>=s; i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, a, b, w;
    cin >> n >> a >> b;

    bool mi = false, ma = false;
    f (i, 0, n - 1) {
        cin >> w;
        if (w == a) mi = true;
        else if (w == b) ma = true;
    }

    if (mi && ma) {
        cf (i, a, b) {
            cout << i << endl;
        }
    } else if (mi && !ma) {
        cout << b << endl;
    } else if (!mi && ma) {
        cout << a << endl;
    } else {
        cout << "-1\n";
    }
}
```
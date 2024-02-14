---
type:
  - competitive-programming
  - kattis
tags:
  - simulation
name: Sun and Moon
---
## _Solution:_
Simulate time steps up until $5000$, checking if the both the sun and moon are in the right location (based on if the parity the time step, modulo the periodicity, is correct).

https://open.kattis.com/problems/sunandmoon
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

    int ds, ys, dm, ym;
    cin >> ds >> ys >> dm >> ym;
    int ms = (ys - ds) % ys, mm = (ym - dm) % ym;
    cf (i, 1, 5001) {
        if (i % ys == ms && i % ym == mm) {
            cout << i << endl;
            return 0;
        }
    }
}
```
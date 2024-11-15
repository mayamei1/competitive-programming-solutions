---
tags:
  - competitive-programming/judges/kattis
name: Bottled-Up Feelings
date: 2024-01-08
---
#competitive-programming/complete-search
#competitive-programming/trivial
## _Solution:_
Search through all possible numbers of the smaller bottle, and check if the left over oil is divisible by the larger bottle ($s-v_2*x_2\equiv0\mod{v_1}$). Start search at the bottom in order to minimize number of bottles.

https://open.kattis.com/problems/bottledup
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

    int s, v1, v2;
    cin >> s >> v1 >> v2;
    
    bool solved = false;

    for (int i2 = 0; i2 * v2 <= s; i2++) {
        int left = s - i2 * v2;
        if (left % v1 == 0) {
            solved = true;
            cout << (left / v1) << ' ' << i2;
            break;
        }
    }
    
    if (!solved) {
        cout << "Impossible";
    }
}
```
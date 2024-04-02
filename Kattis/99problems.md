---
tags:
  - competitive-programming/catalog/kattis
name: 99 Problems
---
#competitive-programming/complete-search #competitive-programming/trivial 
## _Solution:_
Iterate through each possible number that ends with $99$, and find the one that has the smallest difference with $n$. 

https://open.kattis.com/problems/99problems
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

    int n;
    cin >> n;

    // 1000
    //
    int min_diff = 1000000, min_i = -1;
    for (int i = 99; i <= 9999; i += 100) {
        if (abs(i - n) <= min_diff) {
            min_i = i;
            min_diff = abs(i - n);
        }
    }

    cout << min_i;
}
```
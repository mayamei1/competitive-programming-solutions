---
tags:
  - competitive-programming/judges/kattis
name: Streets Ahead
date: 2024-02-26
---
#competitive-programming/data-representation #competitive-programming/trivial 
## _Solution:_
Map each street to an ID in the order of the input, then for each query, calculate difference of ID minus 1.

https://open.kattis.com/problems/streetsahead
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

    int n, q;
    cin >> n >> q;

    umap<string, int> id;
    f (i, 0, n) {
        string s;
        cin >> s;
        id[s] = i;
    }

    f (i, 0, q) {
        string s1, s2;
        cin >> s1 >> s2;

        cout << abs(id[s1] - id[s2]) - 1 << endl;
    }
}
```
---
tags:
  - competitive-programming/catalog/kattis
name: Pivot
---
#competitive-programming/data-representation 
## _Solution:_
Given $a$, Assign each number to be the indexed ordering if the numbers were sorted, $b$. Then, for each potential pivot point $b_i$, it is a pivot if $i=b_i$ and $b_i$ is larger than every number to the left of it.

https://open.kattis.com/problems/pivot
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

bool comp(ii& a, ii& b) {
    return a.first < b.first;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vii a(n);
    f (i, 0, n) {
        cin >> a[i].first;
        a[i].second = i;
    }

    sort(a.begin(), a.end());

    vi b(n);
    f (i, 0, n) {
        b[a[i].second] = i;        
    }

    int ma = -1, cnt = 0;
    f (i, 0, n) {
        ma = max(ma, b[i]);
        if (b[i] == i && ma <= b[i]) cnt++;
    }

    cout << cnt;
}
```
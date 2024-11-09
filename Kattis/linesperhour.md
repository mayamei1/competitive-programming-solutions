---
tags:
  - competitive-programming/judges/kattis
name: Lines Per Hour
date: 2024-01-29
---
#competitive-programming/sorting
## _Solution:_
Sort problems by their lines of code, then pick the shortest ones right until it goes over $5$ times fastest lines per hour.

https://open.kattis.com/problems/linesperhour
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

    int n, lph;
    cin >> n >> lph;
    lph *= 5;
    vi ans(n);
    f (i, 0, n) {
        cin >> ans[i];
    }
    sort(ans.begin(), ans.end());

    int sum = 0, i = 0, cnt = 0;
    while (i < n) {
        if ((sum + ans[i]) <= lph) {
            sum += ans[i];
            cnt++;
        }
        else break;
        i++;
    }
    cout << cnt << endl;
}
```
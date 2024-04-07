---
tags:
  - competitive-programming/catalog/kattis
name: ICPC Team Generation
---
#competitive-programming/greedy 
## _Solution:_
Iterate through each rank and pick the two ranks around it. As long as $a_{i+1}\leq i-1$ and $i+1\leq a_{i-1}$, then a team can be made. If a team is made, then skip over to the next rank with the two around them that aren't in a team.

https://open.kattis.com/problems/icpcteamgeneration
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vi aa(n + 1), bb(n + 1);
    cf (i, 1, n) {
        int a, b;
        cin >> a >> b;
        aa[i] = a;
        bb[i] = b;
    }

    int ans = 0;
    cf (i, 2, n - 1) {
        if (aa[i + 1] <= i - 1 && i + 1 <= bb[i - 1]) {
            ans++;
            i += 2;
        }
    }
    cout << ans << endl;
}
```
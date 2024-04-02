---
tags:
  - competitive-programming/catalog/kattis
name: Lockout
---
#competitive-programming/greedy 
## _Solution:_
Three cases

$a_0>\sum\limits a_i-a_0$
- You have to contest $a_0$. This is a $0.5$ chance of winning.
$a_0<\sum\limits a_i-a_0$
- It is guaranteed that you can win by skipping the first world, and guarantee the other worlds.
$a_0=\sum\limits a_i-a_0$
- You have to contest for $a_0$, and try to guarantee another world. If $n=2$, then it is impossible to guarantee another world, so you have to contest for $a_1$ as well. If not, you can guarantee another world.

https://open.kattis.com/problems/lockout
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
#define vi vector<ll>
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

    vi a(n);
    f (i, 0, n) {
        cin >> a[i];
    }
    
    ll t;
    f (i, 0, n) {
        cin >> t;
    }

    vi p(n);
    f (i, 0, n) {
        cin >> p[i];
        p[i]--;
    }

    ll sum = 0;
    f (i, 0, n) sum += a[i];

    if (a[p[0]] > (sum - a[p[0]])) {
        cout << "0.5" << endl;
        f (i, 0, n)
            cout << (p[i] + 1) << ' ';
        cout << endl;
    } else if (a[p[0]] < (sum - a[p[0]])) {
        cout << "1" << endl;
        f (i, 1, n)
            cout << (p[i] + 1) << ' ';
        cout << (p[0] + 1) << endl;
    } else {
        if (n == 2)
            cout << "0.25" << endl;
        else
            cout << "0.5" << endl;
        f (i, 0, n)
            cout << (p[i] + 1) << ' ';
        cout << endl;
    }
}
```
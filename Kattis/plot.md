---
type:
  - competitive-programming
  - kattis
tags:
  - math/polynomials/horner
  - dp
  - math/polynomials/pascals-triangle
name: Plotting Polynomials
---
## _Solution:_
The accumulation of $C$ values results in with frequencies that follow the Pascal's triangle. Calculate $p(x)$ for $0 \le x\le n$ with [[Polynomials#Horner's Method|Horner's method]], and with each iteration, calculate $C_x$ with the previous $C_{1\le x \le n}$ values.

https://open.kattis.com/problems/plot
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

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

#define LSOne(S) ((S) & -(S))

vi p;
int n;
int solve_poly(int x) {
    int ans = p[n];
    rf (i, n, 0) {
        ans = ans * x + p[i];
    }

    return ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;
    p = vi(n + 1);

    cf (i, 0, n) {
        cin >> p[i];
    }
    reverse(p.begin(), p.end());

    vi c(n + 1);
    c[0] = p[0];
    vi pasc = {1, 1};
    vi n_pasc;

    cf (i, 1, n) {
        int ci = solve_poly(i);

        f (j, 0, i) {
            ci -= c[j] * pasc[j];
        }

        c[i] = ci / pasc[i];

        n_pasc = vi();
        n_pasc.push_back(1);
        f (j, 1, pasc.size()) {
            n_pasc.push_back(pasc[j] + pasc[j - 1]);
        }
        n_pasc.push_back(1);
        pasc.swap(n_pasc);
    }

    f (i, 0, n + 1) {
        cout << c[i] << ' ';
    }
    cout << '\n';
}
```
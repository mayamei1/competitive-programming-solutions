---
tags:
  - competitive-programming/catalog/ieeextreme
name: Happy Numbers
---
#competitive-programming/dp/recursive
## _Solution:_
Drawing influence from the algorithm to [find number of happy numbers <= 10^n (OEIS)](https://oeis.org/A068571 "https://oeis.org/A068571"), an observation can be found with the bound $10^{16}$. One step into finding out of a number is a happy number, the maximum possible value is $9^2+9^2+\dots+9^2$ or $81\times16=1296$. This means that if we previously knew every happy number up to $1300$, we could tell if any number is a happy number or not.

If we had some function that could tell the number of happy functions between $0\dots n$, then we can use a prefix sum approach and subtract upper bound by lower bound.

The solution to this problem is a recursive function $h(n,x,f)$. $h$ denotes the number of happy numbers of digit length $n$ where the sum of the digits squared is $x$. The OEIS algorithm had something similar $h(n,x)$. The function was defined as the following:
$h(n,x)=h(n-1, x-0^2)+h(n-1, x-1^2)+...h(n-1,x-9^2)$. 

Then another function iterated through every happy number between $x=1\dots81n$ and summed up $h(n,x)$, plus one for $10^n$.

In this problem, however, we can not always iterate $h(n-1,x-(0\dots9)^2)$, as there is an upper bound that isn't $10^n$, meaning the $n$th digit could only go up to the bound's corresponding digit. To account for this a boolean value $f$ is used to denote whether to "follow" the bound's corresponding digit or not. This is useful, as if the $n$th digit was less than the bound's corresponding digit, then all $0...n-1$ digits afterwards can be any digit. $f$ is only true when finding how many happy numbers there are close to the bound. If, at any point, $f$ is set to false in a recursive path, it will not be set back to true, as it "stepped away" from the bound and no longer is limited by digits.

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

vi d;

struct state {
    int n;
    int x;
    bool follow;

    bool operator==(const state& p) const {
        return (n == p.n && x == p.x && follow == p.follow);
    }
};

struct hash_ {
    size_t operator()(const state& p) const {
        auto hash1 = hash<int>{}(p.n);
        auto hash2 = hash<int>{}(p.x);
        auto hash3 = hash<bool>{}(p.follow);
        auto tmp = hash1 ^ (hash2 * (hash1 != hash2));
        return tmp ^ (hash3 * (tmp != hash3));
    }
};

umap<state, ll, hash_> memo;

ll h(int n, int x, bool follow) {
    if (n < 0 || x < 0) return 0;
    state s = {n, x, follow};
    if (memo.find(s) != memo.end()) return memo[s];

    if (n == 0 && x == 0) {
        return 1;
    }
    if (n == 0 && x != 0) {
        return 0;
    }
    if (n != 0 && x == 0) {
        return 1;
    }

    ll sum = 0;
    if (follow) {
        int di = d[n - 1];
        sum += h(n - 1, x - di * di, true);
        f (i, 0, di) {
            sum += h(n - 1, x - i * i, false);
        }
    } else {
        cf (i, 0, 9) {
            sum += h(n - 1, x - i * i, false);
        }
    }

    memo[s] = sum;
    return memo[s];
}

vi hn;
void precalc() {
    for (int i = 1; i <= 1296; i++) {
        uset<int> visited;
        int a = i;
        while (a != 1 && visited.find(a) == visited.end()) {
            visited.insert(a);
            int next_a = 0, tmp = a;

            while (tmp) {
                int di = tmp % 10;
                next_a += di * di;
                tmp /= 10;
            }

            a = next_a;
        }

        if (a == 1) {
            hn.push_back(i);
        }
    }
}

ll solve(ll bound) {
    d = vi();
    ll tmp = bound;
    while (tmp) {
        int di = tmp % 10;
        d.push_back(di);
        tmp /= 10;
    }

    ll sum = 0;
    memo.clear();
    for (int i = 0; i < hn.size(); i++) {
        sum += h(d.size(), hn[i], true);
    }

    return sum;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    precalc();

    ll a, b;
    cin >> a >> b;

    ll a_count = solve(a-1), b_count = solve(b);
    cout << (b_count - a_count);
}
```
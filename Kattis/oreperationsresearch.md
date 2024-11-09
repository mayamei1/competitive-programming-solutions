---
tags:
  - competitive-programming/judges/kattis
name: Oreperations Research
date: 2024-06-25
---
#competitive-programming/math/gcd/diophantine-equation #competitive-programming/dp 
## _Solution:_
We will define $a_t=\sum\limits a_i$, and $b_t$ likewise. We will also define $\mathrm{sum}_a(i,j)$ as the cyclic sum from $i$ to $j-1$ inclusive, and $\mathrm{sum}_b(i,j)$ likewise. Say for some train car $c_k$, we had cart $i_a$ at the front of $A$ and cart $i_b$ on $B$, and we were to cycle through $x\ge0$ times through $A$ and $y\ge0$ times through $B$, and finally end on carts $j_a$ and $j_b$. Then, it must be true that $a_{t}x+\mathrm{sum}_a(i_{a},j_{a})+b_{t}y+\mathrm{sum}_b(i_{b},j_{b})=c_k$. Moving the equation around to $a_{t}x+b_{t}y=c_k-\mathrm{sum}_a(i_{a},j_{a})-\mathrm{sum}_b(i_{b},j_{b})$, we can see that this is a linear Diophantine equation, where $x$ and $y$ are the unknown. If there exists $x$ and $y$ such that $x\ge0$ and $y\ge0$, then it is possible to start and end on those configurations. For the first train car, $i_a=0$ and $i_b=0$, and we will iterate through $j_a$ and $j_b$ to find valid starting cart configurations for the next train car. For the rest of the train cars, iterate through $i_a$ and $i_b$, and for each valid starting configuration, iterate through $j_a$ and $j_b$ to find the valid starting cart configurations for the next train car. If there are valid starting cart configurations after going through every cart, then the answer is yes.

https://open.kattis.com/problems/oreperationsresearch
```cpp
#include <bits/stdc++.h>

#define ll long long
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

const int N = 100 + 2;
const int A = 50 + 2;
ll c[N];
ll a[A];
ll ra[A];
ll b[A];
ll rb[A];
bool dp[N][A][A];

ll extended_gcd(ll a, ll b, ll& x, ll& y) {
    if (a == 0) {
        x = 0;
        y = 1;
        return b;
    }

    ll x1, y1;
    ll gcd = extended_gcd(b % a, a, x1, y1);
    x = y1 - (b / a) * x1;
    y = x1;

    return gcd;
}

bool check(ll a, ll b, ll c, ll x0, ll y0, ll g) {
    if (c % g) return false;

    x0 *= c / g;
    y0 *= c / g;
    
    if (x0 >= 0 && y0 >= 0) return true;

    ll x, y;
    if (x0 < 0) {
        ll k = y0 / (a / g);
        x = x0 + k * b / g;
        y = y0 - k * a / g;
    } else if (y0 < 0) {
        ll k = x0 / (b / g);
        x = x0 - k * b / g;
        y = y0 + k * a / g;
    }

    return (x >= 0 && y >= 0);
}

ll asum(int l, int r) {
    if (l >= r) return 0;
    if (l == 0) return ra[r - 1];
    return ra[r - 1] - ra[l - 1];
}

ll bsum(int l, int r) {
    if (l >= r) return 0;
    if (l == 0) return rb[r - 1];
    return rb[r - 1] - rb[l - 1];
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int r, s, n;
    cin >> r >> s >> n;

    for (int i = 0; i < r; i++) {
        cin >> a[i];
    }

    for (int i = 0; i < s; i++) {
        cin >> b[i];
    }

    for (int i = 0; i < n; i++) {
        cin >> c[i];
    }

    ll sum = 0;
    for (int i = 0; i < r; i++) {
        sum += a[i];
        ra[i] = sum;
    }

    sum = 0;
    for (int i = 0; i < s; i++) {
        sum += b[i];
        rb[i] = sum;
    }

    ll at = ra[r - 1], bt = rb[s - 1];
    ll x0, y0, g;
    g = extended_gcd(at, bt, x0, y0);

    memset(dp, false, sizeof(dp));
    // c[0]
    for (int ae = 0; ae < r; ae++) {
        for (int be = 0; be < s; be++) {
            ll left = c[0];
            if (ae) left -= asum(0, ae);
            if (be) left -= bsum(0, be);
            bool con1 = left == 0;
            bool con2 = left > 0 && check(at, bt, left, x0, y0, g);
            dp[0][ae][be] = con1 || con2;
        }
    }

    for (int i = 1; i < n; i++) {
        for (int as = 0; as < r; as++) {
            for (int bs = 0; bs < s; bs++) {
                if (!dp[i - 1][as][bs]) continue;
                for (int ae = 0; ae < r; ae++) {
                    for (int be = 0; be < s; be++) {
                        if (dp[i][ae][be]) continue;
                        ll left = c[i];
                        if (as < ae) left -= asum(as, ae);
                        else if (as > ae) left -= asum(as, r) + asum(0, ae);
                        if (bs < be) left -= bsum(bs, be);
                        else if (bs > be) left -= bsum(bs, s) + bsum(0, be);
                        
                        bool con1 = left == 0;
                        bool con2 = left > 0 && check(at, bt, left, x0, y0, g);
                        dp[i][ae][be] = con1 || con2;
                    }
                }
            }
        }
    }

    for (int ae = 0; ae < r; ae++) {
        for (int be = 0; be < s; be++) {
            if (dp[n-1][ae][be]) {
                cout << "Yes" << endl;
                return 0;
            }
        }
    }

    cout << "No" << endl;
}
```
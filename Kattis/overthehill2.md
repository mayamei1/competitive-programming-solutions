---
tags:
  - competitive-programming/judges/kattis
name: Over the Hill, Part 2
date: 2024-06-26
---
#competitive-programming/math/gauss-jordan #competitive-programming/math/modular-arithmetic 
## _Solution:_
Let $m$ be the length of the plain text $a$ and the cipher text $b$. Each column vector performs dot products with the $n$ rows in the matrix, resulting in $\frac{m}{n}$ equations for each row. The $i$-th row has equations in the form $a_{nk+1}\cdot m_{i,1}+a_{nk+2}\cdot m_{i,2}+\cdots+a_{nk+n}\cdot m_{i,n}=b_{nk+i}$, for $0\le k<\frac{m}{n}$. So, each row in the matrix has a system of equations that needs to be solved. If any of the system has no solution, then the final answer has no solution. If there are no 0 solution systems and at least one infinite solution system, then the final answer has too many solutions. If none of the solutions have neither no solution nor infinite solutions, then there is only one solution for the answer.

https://open.kattis.com/problems/overthehill2
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

int n;
string a, b;

#define MOD 37
ll mod(ll a) {
    return ((a % MOD) + MOD) % MOD;
}

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

ll inv(ll b) {
    ll x, y;
    ll d = extended_gcd(b, MOD, x, y);
    if (d != 1) return -1;
    return mod(x);
}

int gauss(vvi a, vi& ans) {
    int n = a.size(), m = a[0].size() - 1;

    vector<int> where(m, -1);
    for (int col = 0, row = 0; col < m && row < n; col++) {
        int sel = row;
        for (int i = row; i < n; i++) {
            if (abs(a[i][col]) > abs(a[sel][col]))
                sel = i;
        }
        if (a[sel][col] == 0) continue;
        for (int i = col; i <= m; i++)
            swap(a[sel][i], a[row][i]);
        where[col] = row;
        for (int i = 0; i < n; i++) {
            if (i != row) {
                dd c = mod(a[i][col] * inv(a[row][col]));
                for (int j = col; j <= m; j++) {
                    a[i][j] = mod(a[i][j] - mod(a[row][j] * c));
                }
            }
        }

        row++;
    }

    ans.assign(m, 0);
    for (int i = 0; i < m; i++) {
        if (where[i] != -1) {
            ans[i] = mod(a[where[i]][m] * inv(a[where[i]][i]));
        }
    }
    
    for (int i = 0; i < n; i++) {
        dd sum = 0;
        for (int j = 0; j < m; j++) {
            sum = mod(sum + mod(ans[j] * a[i][j]));
        }
        if (sum != a[i][m]) return 0;
    }

    for (int i = 0; i < m; i++) {
        if (where[i] == -1) return 2;
    }

    return 1;
}

int encode(char c) {
    if ('A' <= c && c <= 'Z') return (c - 'A');
    if ('0' <= c && c <= '9') return (c - '0') + 26;
    return 36;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;
    getline(cin, a);
    getline(cin, a);
    getline(cin, b);

    vi aa;
    vi bb;
    for (int i = 0; i < a.size(); i++) {
        aa.push_back(encode(a[i]));
    }

    for (int i = 0; i < b.size(); i++) {
        bb.push_back(encode(b[i]));
    }

    int m = aa.size() / n;
    vvi ans(n);
    int inf = false;
    for (int row = 0; row < n; row++) {
        vvi eqx(m);
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                eqx[i].push_back(aa[i * n + j]);
            }
            eqx[i].push_back(bb[i * n + row]);
        }

        int sol = gauss(eqx, ans[row]);

        if (sol == 0) {
            cout << "No solution" << endl;
            return 0;
        } else if (sol == 2) {
            inf = true;
        }
    }

    if (inf) {
        cout << "Too many solutions" << endl;
        return 0;
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << ans[i][j] << ' ';
        }
        cout << endl;
    }
}
```
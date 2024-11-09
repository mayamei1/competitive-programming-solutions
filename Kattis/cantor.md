---
tags:
  - competitive-programming/judges/kattis
name: Cantor
date: 2019-03-01
---
#competitive-programming/math 
## _Solution:_
A ternary expansion is defined as
$$
x=\frac{x_{1}}{3^{1}}+\frac{x_{2}}{3^{2}}+\frac{x_{3}}{3^{3}}+\cdots
$$
where $x_i={0,1,2}$. The representation in the problem is the concatenation of all $x_i$. Since $x$ has finite precision, it is guaranteed that there will be repeating decimal. Multiply by $3$, such that you get
$$
3x=x_{1}+\frac{x_{2}}{3^{2}}+\frac{x_{3}}{3^{3}}+\cdots
$$
Then, the integer part of this number should be $x_1$, while the decimal part is the other terms. Keep multiplying by $3$ until you either come across a $1$ (not part of the Cantor set), or the decimal part has already been seen before, as it has reached the part of the decimal that will repeat.

https://open.kattis.com/problems/cantor
```cpp
#include <bits/stdc++.h>

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

    string s;
    while (cin >> s && s != "END") {
        if (s == "0" || s == "1") {
            cout << "MEMBER" << endl;
            continue;
        }

        int v = 0;
        s = s.substr(s.find('.') + 1);
        int n = s.size();
        for (int i = 0; i < 6; i++) {
            v *= 10;
            if (i < n) v += s[i] - '0';
        }

        int off = 1000000;

        uset<int> vis;
        bool fail = false;
        while (vis.find(v) == vis.end()) {
            vis.insert(v);
            v *= 3;
            if (v / off == 1) {
                cout << "NON-MEMBER" << endl;
                fail = true;
                break;
            }
            v %= off;
        }
        if (!fail) cout << "MEMBER" << endl;
    }
}
```
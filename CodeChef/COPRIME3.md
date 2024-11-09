---
tags:
  - competitive-programming/judges/codechef
name: Coprime Triples
date: 2024-09-21
---
#competitive-programming/math/number-theory/mobius-inversion #competitive-programming/math/gcd #competitive-programming/math/combinatorics 
## _Solution:_
The problem can be solved via this expression
$$
\begin{align*}
\sum\limits_{a,b,c\in A;a\ne b;b\ne c;a\ne c}[\gcd(a,b,c)=1]\\
&=\sum\limits_{a\in A;d|a}\sum\limits_{b\in A;a\ne b;d|b}\sum\limits_{c\in A;a\ne c;b\ne c;d|c}[\gcd(a,b,c)=1]\\
\end{align*}
$$
Applying Mobius inversion, we get
$$
\begin{align*}
&=\sum\limits_{a\in A;d|a}\sum\limits_{b\in A;a\ne b;d|b}\sum\limits_{c\in A;a\ne c;b\ne c;d|c}\sum\limits_{d}[d|\gcd(a,b,c)]\mu(d)\\
&=\sum\limits_{a\in A;d|a}\sum\limits_{b\in A;a\ne b;d|b}\sum\limits_{c\in A;a\ne c;b\ne c;d|c}\sum\limits_{d}[d|a][d|b][d|c]\mu(d)\\
&=\sum\limits_{d}\mu(d)\sum\limits_{a\in A;d|a}\sum\limits_{b\in A;a\ne b;d|b}\sum\limits_{c\in A;a\ne c;b\ne c;d|c}1\\
\end{align*}
$$
Let $g(d)$ be the number of elements divisible by $d$.
$$
\begin{align*}
&=\sum\limits_{d}\mu(d)\frac{g(d)(g(d)-1)(g(d)-2)}{6}
\end{align*}
$$
Finding $g(d)$ for all positive integers up to $d$ can be fount in $O(d\log(d))$ time. Solving for all $\mu(d)$ can be done in $O(d)$ time. And solving for the above equation is $O(d)$ time.

https://www.codechef.com/problems/COPRIME3
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = int;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

void solve() {
    int n;
    cin >> n;

    int X = 1e6;
    vi cnt(X + 1);
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;
        cnt[x]++;
    }

    vi g(X + 1);
    for (int d = 1; d <= X; d++) {
        for (int k = 1; k * d <= X; k++) {
            g[d] += cnt[k * d];
        }
    }

    vi primes;
    vi comp(X + 1);
    vi mu(X + 1);
    mu[1] = 1;
    for (int i = 2; i <= X; i++) {
        if (!comp[i]) {
            primes.push_back(i);
            mu[i] = -1;
        }
        for (int p : primes) {
            int j = i * p;
            if (j > X) break;
            comp[j] = 1;
            if (i % p) {
                mu[j] = mu[i] * mu[p];
            } else {
                mu[j] = 0;
            }
        }
    }

    ll ans = 0;
    for (int d = 1; d <= X; d++) {
        ans += 1ll * mu[d] * g[d] * (g[d] - 1) * (g[d] - 2) / 6;
    }
    cout << ans << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
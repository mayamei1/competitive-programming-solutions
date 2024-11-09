---
tags:
  - competitive-programming/judges/codechef
name: Simple Sum
date: 2024-09-21
---
#competitive-programming/math/number-theory/mobius-inversion #competitive-programming/math/number-theory/eulers-phi #competitive-programming/math/gcd 
## _Solution:_
We can make use of the fact that $f(n)$ is a multiplicative function to generate a sieve to solve all $f(n)$ up to $10^7$.
$$
\begin{align*}
f(n)=\sum\limits_{i=1}^{n} \frac{n}{\gcd(i,n)}
\end{align*}
$$
With $k=\gcd(i,n)$,
$$
\begin{align*}
f(n)&=\sum\limits_{k=1}^{n}\sum\limits_{i=1}^{n}[\gcd(i,n)=k] \frac{n}{k}\\
&=\sum\limits_{k=1}^{n}\sum\limits_{i=1}^{n}[\gcd(\frac{i}{k},\frac{n}{k})=1] \frac{n}{k}\\
\end{align*}
$$
With $i=ak$,
$$
\begin{align*}
&=\sum\limits_{k=1}^{n}\sum\limits_{a=1}^{\lfloor \frac{n}{k}\rfloor}[\gcd(a,\frac{n}{k})=1] \frac{n}{k}
\end{align*}
$$
Applying Mobius inversion,
$$
\begin{align*}
&=\sum\limits_{k=1}^{n}\sum\limits_{a=1}^{\lfloor \frac{n}{k}\rfloor}\sum\limits_{d=1}^{\lfloor \frac{n}{k}\rfloor}[d|a][dk|n]\mu(d) \frac{n}{k}\\
&=\sum\limits_{k=1}^{n}\sum\limits_{d=1}^{\lfloor \frac{n}{k}\rfloor}[dk|n]\mu(d) \frac{n}{k}\sum\limits_{a=1}^{\lfloor \frac{n}{k}\rfloor}[d|a]\\
&=\sum\limits_{k=1}^{n}\sum\limits_{d=1}^{\lfloor \frac{n}{k}\rfloor}[dk|n]\mu(d) \frac{n}{k}\lfloor \frac{n}{dk}\rfloor\\
&=\sum\limits_{k=1}^{n}\sum\limits_{d=1}^{\lfloor \frac{n}{k}\rfloor}[dk|n]\mu(d) \frac{n}{k}\lfloor \frac{n}{dk}\rfloor\\
&=\sum\limits_{k|n}\sum\limits_{d| \frac{n}{k}}\mu(d) \frac{n}{k}\frac{n}{dk}\\
\end{align*}
$$
With symmetry, we can replace $\frac{n}{k}$ with $k$.
$$
\begin{align*}
&=\sum\limits_{k|n}\sum\limits_{d|k}\mu(d) \frac{k^{2}}{d}\\
&=\sum\limits_{k|n}k\sum\limits_{d|k}\mu(d) \frac{k}{d}\\
\end{align*}
$$
With $\sum\limits_{d|k}\mu(d) \frac{k}{d}=\phi(k)$,
$$
\begin{align*}
&=\sum\limits_{k|n}k \phi(k)
\end{align*}
$$
Let's extract some prime factor $p$ out from $k$. If $n=mp^{e}$, then every $k$ can be denoted as $lp^a$.
$$
\begin{align*}
&=\sum\limits_{a=0}^e\sum\limits_{l|m}lp^{a}\phi(l\phi^{a})\\
&=\sum\limits_{a=0}^{e}p^{a}\phi(p^{a})\sum\limits_{l|m}l\phi(l)
\end{align*}
$$
Thus, we get
$$
f(p^e)=\sum\limits_{a=0}^{e}p^{a}\phi(p^{a})
$$
This can be calculated via a linear sieve. Say we keep track of $g(q)=f(p^{k})$, where $p$ is the smallest prime that divides $q$. And, we keep track of $h(q)=p^e$, where $p^e$ is the maximal prime power. When $q$ is prime, we can set $h(q)=q$ and $g(q)=1+h(q)\cdot\phi(h(q))$. Since $q$ has one prime, $f(q)=g(q)$. For $q=ip$ and $p\nmid i$, then $h(q)=p$ and $g(q)=g(p)$. Since $i$ and $p$ are coprime, $f(q)=f(i)\cdot f(p)$. For $q=ip$ and $p|i$, then $h(q)=h(q)\cdot p$ and $g(q)=g(i)+h(i)\cdot\phi(h(i))$. Then, $f(q)=f(i)\cdot \frac{g(q)}{g(i)}$, or in other words, dividing out the old $f(p^{k-1})$ and multiplying back in the new $f(p^k)$.

https://www.codechef.com/problems/SMPLSUM
```cpp
#include <bits/stdc++.h>

using namespace std;

using ll = long long;
using dd = ll;
using ii = pair<dd, dd>;
using vi =  vector<dd>;
using vii = vector<ii>;
using vvi = vector<vi>;
using vvii = vector<vii>;

vi primes;
vector<bool> comp;
vi f;
vi phi;
vi pa;
vi sum;

void sieve(ll n) {
    comp.assign(n + 1, false);
    primes.clear();
    f.assign(n + 1, 0);
    phi.assign(n + 1, 0);
    pa.assign(n + 1, 0);
    sum.assign(n + 1, 0);

    f[1] = 1, phi[1] = 1;
    for (ll i = 2; i <= n; i++) {
        if (!comp[i]) {
            primes.push_back(i);
            phi[i] = i - 1;
            pa[i] = i;
            sum[i] = 1 + pa[i] * phi[pa[i]];
            f[i] = sum[i];
        }
        for (ll p : primes) {
            int j = i * p;
            if (j > n) break;
            comp[j] = true;
            if (i % p) {
                phi[j] = phi[i] * phi[p];
                pa[j] = p;
                sum[j] = sum[p];
                f[j] = f[i] * f[p];
            } else {
                phi[j] = p * phi[i];
                pa[j] = p * pa[i];
                sum[j] = sum[i] + pa[j] * phi[pa[j]];
                f[j] = f[i] / sum[i] * sum[j];
                break;
            }
        }
    }
}

void solve() {
    int n;
    cin >> n;

    printf("%lld\n", f[n]);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    sieve(1e7);

    int t;
    cin >> t;

    while (t--) solve();
}
```
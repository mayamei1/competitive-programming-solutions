---
type:
  - competitive-programming
  - kattis
tags:
  - graph/tree
  - graph/dfs
  - sorting
  - dp
name: Citations
---
## _Solution:_
For any particular subtree, imagine that the children are already optimal, meaning that the child's subtree minimizes the total delay time of its particular subtree. You can treat the entire vertex/book as two values: the total time it takes to read this book and the number of books in this tree (including the original). With the optimal children, you can build up the optimal parent.

A simple case to think about is with a list of books with no citations. There is guaranteed delay from reading the book, but let's ignore that for now. The first book ($r_1$ read time) will have $0$ *extra* delay, second will have the $r_1$ extra delay, third will have $r_1+r_2$ extra delay, etc. Observe that once all of the extra delay is added up, $r_1$ will have the most influence on the total, followed by $r_2$, $r_3$, etc. So you would want to put the lowest read time to be $r_1$, second lowest for $r_2$, and so on<sup>1</sup>.

Let's think about a case with varying citation sizes. Now, we have to worry about the fact that the extra delay not only applies to the original book, but also every book in the tree as well. So for any two books, you can calculate and compare the extra delay of if book 1 or book 2 goes first. If read time is $r$ and number of books is $c$, then compare $r_1\times c_2$ (book 1 is first) with $r_2\times c_1$ (book 2 is first). Finally, you will need to convince yourself that with the pairwise compare, you are able to do a full sort<sup>2</sup>.

Finally, once you figure out the correct order for each citation list, run it through once again through DFS to simulate the return time.

<sup>1</sup> If you don't understand why, think about a rectangle that you can vary the side lengths, but has a static perimeter. If you want to maximize surface area, then the best thing you can do is make a square. To minimize, you want one side to be as big as possible, and the other as small as possible.
<sup>2</sup> If it helps, you can rearrange the equation/inequality to $\frac{r_1}{c_1}<\frac{r_2}{c_2}$, and you are sorting by the fraction $\frac{r_i}{c_i}$.

https://open.kattis.com/problems/citations
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

int n;
vector<ll> k;
vvi adj;

struct iii {
    ll v, s, c;
};

bool comp(iii& a, iii& b) {
    return (a.s * b.c) < (b.s * a.c);
}

pair<ll,ll> precalc(int v) {
    if (adj[v].empty()) return {k[v] + 1, 1};
    ll sum = 1 + k[v];
    ll count = 1;
    vector<iii> sub;
    for (int u : adj[v]) {
        pair<ll, ll> val = precalc(u);
        sum += val.first;
        count += val.second;
        sub.push_back({u, val.first, val.second});
    }

    sort(sub.begin(), sub.end(), comp);
    adj[v].clear();
    for (iii s : sub) {
        adj[v].push_back(s.v);
    }
    
    return {sum, count};
}

ll sum = 0, t = 0;
void dfs(int v) {
    t += 1;
    for (int u : adj[v]) {
        dfs(u);        
    }
    t += k[v];
    sum += t;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;

    k = vector<ll>(n);
    adj = vvi(n);
    f (i, 0, n) {
        int f;
        cin >> k[i] >> f;
        f (j, 0, f) {
            int b;
            cin >> b;
            adj[i].push_back(b - 1);
        }
    }

    precalc(0);
    dfs(0);
    cout << sum;
}
```
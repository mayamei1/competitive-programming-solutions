---
tags:
  - competitive-programming/judges/codechef
name: OPME
date: 2024-07-03
---
#competitive-programming/greedy #competitive-programming/data-representation 
## _Solution:_
Say for some $x$ that we are trying to make the only element left, any continuous group of elements that are less than $x$ can be merged into a single element that is less than $x$. Then, if and only if, after the merging, the number of elements more than or equal to $x$ is more than the number of elements less than $x$, then it is possible to end with $x$. First, we will sort each distinct element, and for each distinct element, we keep a list of indices where they exist. We keep track of an array that indicates which elements in $a$ are lower than the current $x$, denoted `vis[i]`. We also keep track of the number of elements that are smaller than $x$, and the number of elements that are larger or equal to $x$, initially, $l=0$ and $ge=n$. Iterating through distinct elements of $a$, we first check if $ge>l$, and if so, add the current element to a set. Then, iterate through the indices where the element exists, and set `vis[i]=true`. You will also increment the number of elements lower than $x$, and decrement the number of elements greater or equal to $x$. If at any point when you set `vis[i]=true`, if either of the neighbors are also true, decrement the number of elements less than $x$ by the number of neighbors that are set true (thus merging them). Finally, iterate through $a$ and check if $a_i$ exists in the set.

https://www.codechef.com/problems/OPME
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

using namespace std;

const int N = 2e5 + 2;
int a[N];
int b[N];
bool vis[N];

bool comp(int i, int j) {
    if (a[i] == a[j]) return i < j;
    return a[i] < a[j];
}

void solve() {
    int n;
    cin >> n;

    for (int i = 0; i < n; i++) cin >> a[i], b[i] = i;
    sort(b, b + n, comp);
    fill(vis, vis + n, 0);

    set<int> ans;
    int hi = n, lo = 0;
    for (int i = 0; i < n; i++) {
        int j = b[i];
        if (hi > lo) ans.insert(a[j]);
        vis[j] = 1;
        hi--;
        lo++;
        if (j > 0 && vis[j - 1]) lo--;
        if (j < (n - 1) && vis[j + 1]) lo--;
    }

    for (int i = 0; i < n; i++) {
        cout << ans.count(a[i]);
    }
    cout << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}

```
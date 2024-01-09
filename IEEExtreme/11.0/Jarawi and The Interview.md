---
type:
  - competitive-programming
  - ieeextreme
tags:
  - string
  - greedy
  - work-backwards
---
#ieeextreme

## _Solution:_
Start by building a list of each index for each character in $s$. For each query, iterate backwards through the string. With each character, greedily try to get the highest possible index without going over the previous iteration's index that has the same letter. This can be found with binary search. If impossible, then the index of the current iteration indicates the start of the largest suffix of $p$.

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
string s, p;
int q;
vvi idx(26, vi());

void precalc() {
    for (int i = 0; s[i]; i++) {
        idx[s[i] - 'a'].push_back(i);
    }
}

int solve() {
    int i;
    int curr = 10000000;
    for (i = p.size() - 1; i >= 0; i--) {
        int c = p[i] - 'a';

        auto itr = upper_bound(idx[c].begin(), idx[c].end(), curr - 1);
        if (itr == idx[c].begin()) break;
        itr--;
        curr = *itr;
    }
    return p.size() - i - 1;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> s;

    precalc();

    cin >> q;
    while (q--) {
        cin >> p;
        cout << solve() << '\n';
    }
}
```
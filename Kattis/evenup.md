---
tags:
  - competitive-programming/catalog/kattis
name: Even Up Solitaire
---
#competitive-programming/simulation
#competitive-programming/ds/stack
## _Solution:_
Iterate through each card, and keep a stack of the "right-most" card. As you get the next card, check if the sum of the new and the right-most cards are even. If so, remove the right-most from the stack. Else insert the new card into the stack.

https://open.kattis.com/problems/evenup
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vi c(n);
    f (i, 0, n) {
        cin >> c[i];
    }

    stack<int> s;
    f (i, 0, n) {
        if (s.empty()) s.push(c[i]);
        else if ((s.top() % 2) == (c[i] % 2)) s.pop();
        else s.push(c[i]);
    }

    cout << s.size();
}
```
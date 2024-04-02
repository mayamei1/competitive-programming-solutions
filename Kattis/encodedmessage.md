---
tags:
  - competitive-programming/catalog/kattis
name: Encoded Message
---
#competitive-programming/string
#competitive-programming/trivial
## _Solution:_
Iterate $0\le i<\sqrt{\lvert s\rvert}$, and get every letter starting at $i$ with jumps of $\sqrt{\lvert s\rvert}$.

https://open.kattis.com/problems/encodedmessage
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int tc;
    cin >> tc;
    while (tc--) {
        string s;
        cin >> s;

        int n = s.size();
        int n2 = sqrt(n);

        string ans = "";
        rf (i, n2, 0) {
            for (int j = i; j < n; j += n2) {
                ans += s[j];
            }
        }
        cout << ans << '\n';
    }
}
```
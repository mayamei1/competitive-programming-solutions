---
tags:
  - competitive-programming/catalog/kattis
name: Permutation Code
---
#competitive-programming/string
#competitive-programming/ad-hoc
## _Solution:_
Keep track of what characters are at which indices for `s` and `p`. Starting at `d`, decode the first letter, then decode at `d-1` using the answer from `d`, and continue until `0`. Then start from `n-1` and decode using the answer from `0`, and continue until `d+1`.

```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>
#include <bitset>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int x;
    while (cin >> x && x) {
        string s, p, c;
        cin >> s >> p >> c;
        int n = c.size();
        int l = s.size();

        unordered_map<char, int> s_i;
        unordered_map<char, int> p_i;
        for (int i = 0; i < l; i++) {
            s_i[s[i]] = i;
            p_i[p[i]] = i;
        }

        int d = ((int)(pow(n, 1.5)) + x) % n;

        vector<char> m(n);
        m[d] = p[s_i[c[d]]];
        for (int i = d - 1; i >= 0; i--) {
            m[i] = p[s_i[c[i]] ^ s_i[m[(i + 1) % m.size()]]];
        }

        for (int i = m.size() - 1; i > d; i--) {
            m[i] = p[s_i[c[i]] ^ s_i[m[(i + 1) % m.size()]]];
        }

        for (int i = 0; i < c.size(); i++) {
            cout << m[i];
        }

        cout << '\n';
    }
}
```
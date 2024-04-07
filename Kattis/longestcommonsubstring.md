---
tags:
  - competitive-programming/catalog/kattis
name: Longest Common Substring
---
#competitive-programming/string/kmp #competitive-programming/complete-search 
## _Solution:_
Try every substring of one string, and compare with the rest with KMP.

https://open.kattis.com/problemslongestcommonsubstring/
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

vi LPS(string p) {
    int n = p.size();
    vi lps(n);
    int len = 0;
    lps[0] = 0;
    int i = 1;
    while (i < n) {
        if (p[i] == p[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len == 0) {
                lps[i] = 0;
                i++;
            } else {
                len = lps[len - 1];
            }
        }
    }

    return lps;
}

bool kmp(string pat, string s) {
    vi lps = LPS(pat);
    int n = s.size(), m = pat.size();
    int i = 0, j = 0;
    while (i < n) {
        if (s[i] == pat[j]) {
            i++;
            j++;
        }

        if (j == m) {
            return true;
            j = lps[j - 1];
        } else if (i < n && pat[j] != s[i]) {
            if (j) j = lps[j - 1];
            else i++;
        }
    }

    return false;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vs ss(n);
    f (i, 0, n) {
        cin >> ss[i];
    }

    int ans = 0;
    for (int i = 0; ss[0][i]; i++) {
        bool fail = false;
        for (int j = 1; ss[0][i + j - 1]; j++) {
            string p = ss[0].substr(i, j);
            
            for (int k = 0; k < n; k++) {
                if (!kmp(p, ss[k])) {
                    fail = true;
                    break;
                }
            }

            if (fail) break;
            else ans = max(ans, j);
        }
    }

    cout << ans << endl;
}
```
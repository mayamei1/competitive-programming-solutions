---
type:
  - competitive-programming
  - ieeextreme
tags:
  - binary-search
  - data-representation
  - string
  - ds/set
---
#ieeextreme 

## _Solution:_
While not explicitly using the standard library set, I have effectively used one. Create a sorted list of dictionary words, as well as a sorted list of reversed string dictionary words. This is to figure out how many words fit a particular prefix or suffix.

For each query word, iterate through possible prefix/suffix combinations. Binary search twice to find the upper and lower bound of dictionary prefixes that match. Do the same for suffixes. If at any point there is a matching prefix and a matching suffix at the same time, then that is a valid combination. However, you need to look out for ambiguity, meaning if there are any other unique pairs of dictionary words, then it is ambiguous.

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

int n, m;
vs dict, rev_dict;
string word;

int match(string pre, vs& d, bool maximize) {
    int l = 0, h = n - 1;
    int extreme = (maximize) ? -1 : n;

    //cout << "search for " << pre << endl;

    while (l <= h) {
        int m = (h - l) / 2 + l;
        //cout << m << ' ' << d[m] << ' ';
        bool match = true;
        for (int i = 0; pre[i]; i++) {
            if (pre[i] > d[m][i]) {
                match = false;
                l = m + 1; 
                //cout << "too low1\n";
                break;
            } else if (pre[i] < d[m][i]) {
                match = false;
                h = m - 1;
                //cout << "too high1\n";
                break;
            }
        }

        if (match) {
            if (maximize) {
                extreme = max(extreme, m);
                l = m + 1;
                //cout << "too low2\n";
            } else {
                extreme = min(extreme, m);
                h = m - 1;
                //cout << "too high2\n";
            }
        }
    }

    return extreme;
}

int check(string& pre, string& suf, int& pre_idx, int& suf_idx) {
    int min_pre = match(pre, dict, false);
    int max_pre = match(pre, dict, true);
    int min_suf = match(suf, rev_dict, false);
    int max_suf = match(suf, rev_dict, true);

    // cout << pre << ' ' << suf << ' ' << min_pre << ' ' << max_pre << ' ' << min_suf << ' ' << max_suf << '\n';

    if (min_pre != n && min_suf != n) {
        if (min_pre == max_pre && min_suf == max_suf) {
            pre_idx = min_pre;
            suf_idx = min_suf;
            return 0;
        } else {
            return 1;
        }
    }

    return -1;
}

void solve() {
    if (word.size() < 5) {
        cout << "none\n";
        return;
    }

    string rev_word = word;
    reverse(rev_word.begin(), rev_word.end());
    
    string pre = word.substr(0, 3);
    string suf = rev_word.substr(0, rev_word.size() - 2);

    int pre_ans = -1, suf_ans = -1;

    for (int mid = 2; ; mid++) {
        int pre_idx = -1, suf_idx = -1;
        int a = check(pre, suf, pre_idx, suf_idx);
        if (a == 1) {
            cout << "ambiguous\n";
            return;
        } else if (a == 0) {
            if (pre_ans != -1) {
                if (pre_ans != pre_idx || suf_ans != suf_idx) {
                    cout << "ambiguous\n";
                    return;
                }
            } else {
                pre_ans = pre_idx;
                suf_ans = suf_idx;
            }
        }

        suf.pop_back();
        if (suf.size() < 3) break;
        a = check(pre, suf, pre_idx, suf_idx);
        if (a == 1) {
            cout << "ambiguous\n";
            return;
        } else if (a == 0) {
            if (pre_ans != -1) {
                if (pre_ans != pre_idx || suf_ans != suf_idx) {
                    cout << "ambiguous\n";
                    return;
                }
            } else {
                pre_ans = pre_idx;
                suf_ans = suf_idx;
            }
        }
        pre.push_back(word[mid + 1]);
    }

    if (pre_ans == -1) cout << "none\n";
    else {
        string tmp = rev_dict[suf_ans];
        reverse(tmp.begin(), tmp.end());
        cout << dict[pre_ans] << ' ' << tmp << '\n';
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    vs test = {"aa", "a"};
    sort(test.begin(), test.end());

    cin >> n >> m;

    dict = vs(n);
    rev_dict = vs(n);
    f (i, 0, n) {
        cin >> word;
        dict[i] = word;
        reverse(word.begin(), word.end());
        rev_dict[i] = word;
    }

    sort(dict.begin(), dict.end());
    sort(rev_dict.begin(), rev_dict.end());

    f (i, 0, m) {
        cin >> word;
        solve();
    }
}
```
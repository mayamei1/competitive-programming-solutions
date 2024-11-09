---
tags:
  - competitive-programming/judges/kattis
name: String Multimatching
date: 2024-11-05
---
#competitive-programming/string/suffix-array #competitive-programming/binary-search 
## _Solution:_
First compute the suffix array of the text with length $n$. Then, for each pattern, we keep track of $l=1$ and $r=n$, denoting the range of suffixes in the suffix array that match the pattern. Do update $(l,r)$, we iterate through each character in the pattern, and binary search the range to find the new $(l,r)$. Then, print every value in the suffix array between $(l,r)$. Note that using `$` for suffix array generation will not suffice, and you can instead use `\01`.

https://open.kattis.com/problems/stringmultimatching
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

vvi c_pow;
vi sort_cyclic_shifts(string const& s, bool saveRanks) {
    int n = s.size();
    const int alphabet = 256;
    vi p(n), c(n), cnt(max(alphabet, n), 0);
    for (int i = 0; i < n; i++)
        cnt[s[i]]++;
    for (int i = 1; i < alphabet; i++)
        cnt[i] += cnt[i-1];
    for (int i = 0; i < n; i++)
        p[--cnt[s[i]]] = i;
    c[p[0]] = 0;
    int classes = 1;
    for (int i = 1; i < n; i++) {
        if (s[p[i]] != s[p[i-1]])
            classes++;
        c[p[i]] = classes - 1;
    }
    if (saveRanks) c_pow.push_back(c);
    vi pn(n), cn(n);
    for (int h = 0; (1 << h) < n; ++h) {
        for (int i = 0; i < n; i++) {
            pn[i] = p[i] - (1 << h);
            if (pn[i] < 0)
                pn[i] += n;
        }
        fill(cnt.begin(), cnt.begin() + classes, 0);
        for (int i = 0; i < n; i++)
            cnt[c[pn[i]]]++;
        for (int i = 1; i < classes; i++)
            cnt[i] += cnt[i-1];
        for (int i = n-1; i >= 0; i--)
            p[--cnt[c[pn[i]]]] = pn[i];
        cn[p[0]] = 0;
        classes = 1;
        for (int i = 1; i < n; i++) {
            ii cur = {c[p[i]], c[(p[i] + (1 << h)) % n]};
            ii prev = {c[p[i-1]], c[(p[i-1] + (1 << h)) % n]};
            if (cur != prev)
                ++classes;
            cn[p[i]] = classes - 1;
        }
        c.swap(cn);
        c_pow.push_back(c);
    }
    return p;
}

vi suffix_array_construction(string s, bool saveRanks) {
    s += "\01";
    vi sorted_shifts = sort_cyclic_shifts(s, saveRanks);
    sorted_shifts.erase(sorted_shifts.begin());
    return sorted_shifts;
}

int n, m;
vi suf;
string s;
string t;

bool lb;
bool comp(int a, int b) {
    int i = a + b;
    if (i >= m) return lb;
    if (lb) return s[i] < t[b];
    return t[a] < s[i];
}

bool solve() {
    if (!(cin >> n)) return false;

    getline(cin, s);
    vector<string> p(n);
    for (string& x : p) {
        getline(cin, x);
    }

    getline(cin, s);
    m = s.size();

    suf = suffix_array_construction(s, false);
    // for (int i = 0; i < m; i++) {
    //     cout << suf[i] << ' ';
    //     for (int j = suf[i]; j < m; j++) {
    //         cout << s[j];
    //     }
    //     cout << endl;
    // }

    for (string& x : p) {
        t = x;
        auto l = suf.begin(), h = suf.end();
        for (int i = 0; i < t.size(); i++) {
            lb = true;
            auto nl = lower_bound(l, h, i, comp);
            lb = false;
            auto nh = upper_bound(l, h, i, comp);
            l = nl, h = nh;
        }
        vi ans;
        while (l != h) ans.push_back(*(l++));
        sort(ans.begin(), ans.end());
        for (int x : ans) cout << x << ' ';
        cout << endl;
    }

    return true;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (solve());
}
```
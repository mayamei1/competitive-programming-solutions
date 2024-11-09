---
tags:
  - competitive-programming/judges/codechef
name: Make My Array Equal
date: 2024-07-31
---
#competitive-programming/math 
## _Solution:_
It can be shown that the only solutions that exist are if the array is already equal, or consists of two distinct elements and one of which is zero. Say we have three or more distinct elements: any attempts to make them equal is impossible, since any operation will always make the element larger than both of the elements. If we had two non-zero elements, the same applies. Obviously, if an array is already equal, then no operations are needed. With two distinct elements, one of which is zero, the sum of zero and the other number is equal to the number (rather than larger than both elements).

https://www.codechef.com/START145B/problems/MEBA
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

void solve() {
    int n;
    cin >> n;

    map<int, int> freq;
    for (int i = 0; i < n; i++) {
        int a;
        cin >> a;
        freq[a]++;
    }

    if (freq.size() > 2) {
        cout << "NO" << endl;
        return;
    }

    if (freq.size() == 1) {
        cout << "YES" << endl;
        return;
    }

    if (freq.begin()->first == 0)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    while (t--) solve();
}
```
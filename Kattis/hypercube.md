---
tags:
  - competitive-programming/judges/kattis
name: Hamiltonian Hypercube
date: 2024-09-09
---
#competitive-programming/math 
## _Solution:_
You can determine the order of a value by looking at the the bits in most significant to least significant order. Keep track of a `flip` variable that is initially false. Looking at the next most significant bit `b`, you will set `ans` at the same bit index to `flip^b`. Then, update flip to be `flip=flip^b`. This is because when you go to the second half of the gray code, the binary values are reversed.

https://open.kattis.com/problems/hypercube
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

int n;
ll decode(string s) {
    ll ans = 0;

    bool flip = false;
    for (int i = 0; i < n; i++) {
        bool b = s[i] == '1';
        ans <<= 1;
        ans += flip ^ b;

        flip = flip ^ b;
    }

    return ans;
}

void solve() {
    cin >> n;

    string sa, sb;
    cin >> sa >> sb;

    ll a = decode(sa), b = decode(sb);

    cout << max(abs(b - a) - 1, 0ll) << endl;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
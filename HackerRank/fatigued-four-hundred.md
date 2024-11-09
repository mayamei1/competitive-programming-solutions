---
tags:
  - competitive-programming/judges/hackerrank
name: Fatigued Four Hundred
date: 2024-10-26
---
#competitive-programming/complete-search 
## _Solution:_
For each swimmer, perform backtracking to try all possibilities of effort.

https://www.hackerrank.com/contests/lpc-2024/challenges/fatigued-four-hundred
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

double t[4];
int ef[] = {75, 80, 85, 90, 95, 100};
double pc[] = {1.16, 1.125, 1.088, 1.055, 1.026, 1.0};
double pr[] = {1.015, 1.022, 1.032, 1.045, 1.06, 1.1};

double mx;
vi mx_path(4);
vi path(4);
void dfs(int c, double sum, double pen) {
    if (c == 4) {
        if (sum < mx) {
            mx_path = path;
            mx = sum;
        }
        return;
    }

    for (int i = 0; i < 6; i++) {
        double next = sum + t[c] * pen * pc[i];
        path[c] = i;
        dfs(c + 1, next, pen * pr[i]);
    }
}

void solve() {
    int n;
    cin >> n;

    for (int i = 0; i < n; i++) {
        mx = 1e10;
        for (int j = 0; j < 4; j++) {
            cin >> t[j];
        }

        dfs(0, 0, 1);
        for (int i : mx_path) {
            printf("%d ", ef[i]);
        }
        printf("%.1f\n", mx);
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    solve();
}
```
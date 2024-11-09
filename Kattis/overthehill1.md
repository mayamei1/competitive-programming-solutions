---
tags:
  - competitive-programming/judges/kattis
name: Over the Hill, Part 1
date: 2024-06-26
---
#competitive-programming/simulation #competitive-programming/math/modular-arithmetic 
## _Solution:_
Run through the described encryption algorithm.

https://open.kattis.com/problems/overthehill1
```cpp
#include <bits/stdc++.h>

#define ll long long
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

using namespace std;

const int N = 10 + 2;
int mat[N][N];

int encode(char c) {
    if ('A' <= c && c <= 'Z') return (c - 'A');
    if ('0' <= c && c <= '9') return (c - '0') + 26;
    return 36;
}

char decode(int a) {
    if (0 <= a && a <= 25) return a + 'A';
    if (26 <= a && a <= 35) return a - 26 + '0';
    return ' ';
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> mat[i][j];
        }
    }

    string s;
    getline(cin, s);
    getline(cin, s);
    int m = s.size();

    string ans;
    for (int i = 0; i < m; i += n) {
        vi col;
        for (int j = i; j < (i + n); j++) {
            if (j < m) col.push_back(encode(s[j]));
            else col.push_back(36);
        }

        for (int j = 0; j < n; j++) {
            int sum = 0;
            for (int k = 0; k < n; k++) {
                sum += mat[j][k] * col[k];
            }
            ans += decode(sum % 37);
        }
    }

    cout << ans << endl;
}
```
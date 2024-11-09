---
tags:
  - competitive-programming/judges/kattis
name: Welcome to Code Jam (Easy)
date: 2019-03-20
---
#competitive-programming/dp #competitive-programming/work-backwards 
## _Solution:_
Check the solution of [[welcomehard]].

https://open.kattis.com/problems/welcomeeasy
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

#define LSOne(S) ((S) & -(S))

#define f(i,s,e) for(ll i=s;i<e;i++)
#define cf(i,s,e) for(ll i=s;i<=e;i++)
#define rf(i,e,s) for(ll i=e-1;i>=s;i--)

using namespace std;

int mod = 10000;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    string p = "welcome to code jam";
    int m = p.size();

    string s;
    getline(cin, s);

    for (int x = 1; x <= t; x++) {
        getline(cin, s);
        int n = s.size();

        vi dp(n), n_dp(n);
        int sum = 0;
        for (int i = n - 1; i >= 0; i--) {
            dp[i] = s[i] == 'm';
        }

        for (int i = m - 2; i >= 0; i--) {
            int sum = 0;
            n_dp.assign(n, 0);
            for (int j = n - 1; j >= 0; j--) {
                sum = (sum + dp[j]) % mod;
                if (s[j] == p[i]) n_dp[j] = sum;
            }

            dp.swap(n_dp);
        }

        int ans = 0;
        for (int i = 0; i < n; i++) {
            ans = (ans + dp[i]) % mod;
        }

        printf("Case #%d: %04d\n", x, ans);
    }
}
```
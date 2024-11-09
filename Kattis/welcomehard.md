---
tags:
  - competitive-programming/judges/kattis
name: Welcome to Code Jam (Hard)
date: 2019-03-20
---
#competitive-programming/dp #competitive-programming/work-backwards 
## _Solution:_
You can keep a DP table that counts how many occurrences there are for the current suffix. It is technically a two state DP table, with the states being the index of the pattern string ("welcome to code jam") and the index of the input string. Lets call it `dp[p][s]`, `p` for pattern index, `s` for input string index. Iterating backwards through the pattern string, you can count how many occurrences there are of the suffix starting at the current pattern index, given that the first letter of the suffix starts at the input string's index. Let's say we are at the "j" (or the suffix "jam") in the pattern string. Then, at every index where there is an "j" in the input string, the count is the sum of the occurrences of the suffix "am" (`dp[i][j]=dp[i-1][j+1...n]`). The base case is with the suffix "m", where the count is $1$ at every location where there is an "m".

However, two optimizations can be done. A space optimization can be done by removing the pattern index state, because we only care about the previous index (keeping track of two `dp[s]`'s and swapping them around). Then, the input string can be iterated backwards, so that you can simply sum up in the second dimension as you fill out the table. Finally, the answer needs to be $\mod{10000}$.

https://open.kattis.com/problems/welcomehard
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
---
tags:
  - competitive-programming/judges/kattis
name: FizzBuzz
date: 2019-03-20
---
#competitive-programming/trivial 
## _Solution:_
Simulate :)

https://open.kattis.com/problems/fizzbuzz
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int x, y, n;
    cin >> x >> y >> n;

    for (int i = 1; i <= n; i++) {
        bool f = i % x == 0;
        bool b = i % y == 0;
        if (f && b) cout << "FizzBuzz";
        else if (f) cout << "Fizz";
        else if (b) cout << "Buzz";
        else cout << i;
        cout << endl;
    }
}
```
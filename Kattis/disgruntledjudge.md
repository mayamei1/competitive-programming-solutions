---
tags:
  - competitive-programming/judges/kattis
name: Disgruntled Judge
date: 2024-02-06
---
#competitive-programming/complete-search
## _Solution:_
Search every possible $(a,b)$ and check if every second generated number matches with the next input.

https://open.kattis.com/problems/disgruntledjudge
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

int A, B;

int next(int x) {
    return (A * x + B) % 10001;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vi input(n);
    f (i, 0, n) {
        cin >> input[i];
    }

    cf (a, 0, 10000) {
        cf (b, 0, 10000) {
            A = a;
            B = b;
            bool ans = true;
            f (i, 1, n) {
                if (next(next(input[i - 1])) != input[i]) {
                    ans = false;
                    break;
                }
            }

            if (ans) {
                f (i, 0, n) cout << next(input[i]) << '\n';
                return 0;
            }
        }
    }
}
```
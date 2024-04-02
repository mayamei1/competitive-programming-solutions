---
tags:
  - competitive-programming/catalog/kattis
name: Beekeeper
---
#competitive-programming/string
#competitive-programming/trivial
## _Solution:_
Find every consecutive pairs of vowels (no triplets or higher), and print string with highest count.

https://open.kattis.com/problems/beekeeper
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


int n;

void solve() {
    string max_s;
    int max_count = 0;

    cin >> max_s;
    for (int i = 0; i < max_s.size(); i++) {
        if (
            (max_s[i] == 'a' && max_s[i + 1] == 'a') ||
            (max_s[i] == 'e' && max_s[i + 1] == 'e') ||
            (max_s[i] == 'i' && max_s[i + 1] == 'i') ||
            (max_s[i] == 'o' && max_s[i + 1] == 'o') ||
            (max_s[i] == 'u' && max_s[i + 1] == 'u') ||
            (max_s[i] == 'y' && max_s[i + 1] == 'y')
        ) {
            max_count++;
        }
    }

    f (i, 0, n - 1) {
        string temp_s;
        int count = 0;
        cin >> temp_s;

        for (int i = 0; i < temp_s.size() - 1; i++) {
            if (
                (temp_s[i] == 'a' && temp_s[i + 1] == 'a') ||
                (temp_s[i] == 'e' && temp_s[i + 1] == 'e') ||
                (temp_s[i] == 'i' && temp_s[i + 1] == 'i') ||
                (temp_s[i] == 'o' && temp_s[i + 1] == 'o') ||
                (temp_s[i] == 'u' && temp_s[i + 1] == 'u') ||
                (temp_s[i] == 'y' && temp_s[i + 1] == 'y')
            ) {
                count++;
            }
        }

        if (count > max_count) {
            max_s = temp_s;
            max_count = count;
        }
    }

    cout << max_s << '\n';
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n && n) {
        solve();
    }
}
```
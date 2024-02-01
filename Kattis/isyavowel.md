---
type:
  - competitive-programming
  - kattis
tags:
  - trivial
  - string
name: Is Y a Vowel?
---
## _Solution:_
Count the number of vowels, if Y is a vowel or not.

https://open.kattis.com/problems/isyavowel
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
#define f(i,s,e) for(ll i = s; i<e; i++)
#define cf(i,s,e) for(ll i=s; i<=e; i++)
#define rf(i,e,s) for(ll i=e-1, i>=s; i--)

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    string s;
    cin >> s;

    int w = 0, wo = 0;
    for (int i = 0; s[i]; i++) {
        if (s[i] == 'a') {
            w++;
            wo++;
        }
        if (s[i] == 'e') {
            w++;
            wo++;
        }
        if (s[i] == 'i') {
            w++;
            wo++;
        }
        if (s[i] == 'o') {
            w++;
            wo++;
        }
        if (s[i] == 'u') {
            w++;
            wo++;
        }
        if (s[i] == 'y') {
            w++;
        }
    }

    cout << wo << ' ' << w << endl;
}
```
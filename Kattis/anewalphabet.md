---
tags:
  - competitive-programming/judges/kattis
name: A New Alphabet
date: 2020-04-10
---
#competitive-programming/trivial #competitive-programming/string 
## _Solution:_
Use a map to encode every letter (upper and lower).

https://open.kattis.com/problems/anewalphabet
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

#define ll long long int
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

    string s;
    getline(cin, s);

    map<char, string> encode {
        {'A', "@"},
        {'B', "8"},
        {'C', "("},
        {'D', "|)"},
        {'E', "3"},
        {'F', "#"},
        {'G', "6"},
        {'H', "[-]"},
        {'I', "|"},
        {'J', "_|"},
        {'K', "|<"},
        {'L', "1"},
        {'M', "[]\\/[]"},
        {'N', "[]\\[]"},
        {'O', "0"},
        {'P', "|D"},
        {'Q', "(,)"},
        {'R', "|Z"},
        {'S', "$"},
        {'T', "']['"},
        {'U', "|_|"},
        {'V', "\\/"},
        {'W', "\\/\\/"},
        {'X', "}{"},
        {'Y', "`/"},
        {'Z', "2"},
        {'a', "@"},
        {'b', "8"},
        {'c', "("},
        {'d', "|)"},
        {'e', "3"},
        {'f', "#"},
        {'g', "6"},
        {'h', "[-]"},
        {'i', "|"},
        {'j', "_|"},
        {'k', "|<"},
        {'l', "1"},
        {'m', "[]\\/[]"},
        {'n', "[]\\[]"},
        {'o', "0"},
        {'p', "|D"},
        {'q', "(,)"},
        {'r', "|Z"},
        {'s', "$"},
        {'t', "']['"},
        {'u', "|_|"},
        {'v', "\\/"},
        {'w', "\\/\\/"},
        {'x', "}{"},
        {'y', "`/"},
        {'z', "2"}
    };

    for (int i = 0; s[i]; i++) {
        if (encode.find(s[i]) == encode.end()) {
            cout << s[i];
        } else {
            cout << encode[s[i]];
        }
    }
}
```
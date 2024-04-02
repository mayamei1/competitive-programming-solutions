---
tags:
  - competitive-programming/catalog/kattis
name: Adding Words
---
#competitive-programming/ds/umap
## _Solution:_
Keep track of two hash-maps for the definition of numbers and the inverse. Make sure to delete overwritten values in the inverse hash-map.

https://open.kattis.com/problems/addingwords
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

#define f(i,s,e) for(long long int i=s;i<e;i++)
#define cf(i,s,e) for(long long int i=s;i<=e;i++)
#define rf(i,e,s) for(long long int i=e-1;i>=s;i--)

using namespace std;

#define LSOne(S) ((S) & -(S))

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    umap<string, int> def;
    umap<int, string> inv;

    string op, var;
    int val, sum;
    while (cin >> op) {
        if (op == "def") {
            cin >> var >> val;
            if (def.find(var) != def.end()) {
                int old = def[var];
                def.erase(var);
                inv.erase(old);
            }
            def[var] = val;
            inv[val] = var;
        } else if (op == "calc") {
            bool unk = false;
            sum = 0;
            string out;
            cin >> var;
            out = var + " ";
            if (def.find(var) == def.end()) {
                unk = true;
            } else {
                sum += def[var];
            }
            while (cin >> op && op != "=") {
                cin >> var;
                out += op + " " + var + " ";
                if (def.find(var) == def.end()) {
                    unk = true;
                } else {
                    if (op == "+") sum += def[var];
                    else sum -= def[var];
                }
            }
            out += "= ";
            if (unk || (inv.find(sum) == inv.end())) {
                cout << out << "unknown\n";
            } else {
                cout << out << inv[sum] << '\n';
            }
        } else {
            def.clear();
            inv.clear();
        }
    }
}
```
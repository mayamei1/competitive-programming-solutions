---
tags:
  - competitive-programming/catalog/kattis
name: 4 thought
---
#competitive-programming/complete-search 
## _Solution:_
Pre-calculate by search all possible combinations of operations and storing the expression into a hash table (if multiple answers, doesn't matter which one). With each query, print out the expression.

https://open.kattis.com/problems/4thought
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

int n, m;
vector<char> curr;
map<int, string> valid;

int eval() {
    queue<int> v, nv;
    v.push(4);
    f (i, 0, 3) {
        v.push(curr[i]);
        v.push(4);
    }

    while (!v.empty()) {
        int left = v.front(); v.pop();
        char op;
        int right;

        while (!v.empty()) {
            op = v.front(); v.pop();

            if (op == '*') {
                right = v.front(); v.pop();
                left *= right;
            } else if (op == '/') {
                right = v.front(); v.pop();
                left /= right;
            } else break;
        }

        nv.push(left);
        if (!v.empty()) nv.push(op);
    }

    int ans = nv.front(); nv.pop();
    while (!nv.empty()) {
        char op = nv.front(); nv.pop();
        int right = nv.front(); nv.pop();

        if (op == '-') ans -= right;
        else ans += right;
    }

    return ans;
}

void search() {
    if (curr.size() == 3) {
        valid[eval()] = string({curr[0], curr[1], curr[2]});
        return;
    }
    
    curr.push_back('+');
    search();
    curr.pop_back();

    curr.push_back('-');
    search();
    curr.pop_back();

    curr.push_back('*');
    search();
    curr.pop_back();

    curr.push_back('/');
    search();
    curr.pop_back();
}

void solve() {
    if (valid.find(n) != valid.end()) {
        string ans = valid[n];
        cout << "4 " << ans[0] << " 4 " << ans[1] << " 4 " << ans[2] << " 4 = " << n << "\n";
    } else cout << "no solution\n";
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    search();
    cin >> m;

    while (m--) {
        cin >> n;
        solve();
    }
}
```
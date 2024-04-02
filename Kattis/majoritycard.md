---
tags:
  - competitive-programming/catalog/kattis
name: Majority Card
---
#competitive-programming/simulation
#competitive-programming/data-representation
#competitive-programming/ds/umap
#competitive-programming/ds/set
#competitive-programming/amortize
## _Solution:_
Keep a "condensed" deque which keeps track of order of the stack. Keep an hash map to keep track of the frequency. Keep track of a set to keep track of the the smallest majority frequency. For each query, you pop out each affected number from the set, update the value, and insert it back in.

A main worry about this problem is the time complexity, since the numbers are large. This solution is amortized $O(n\log{(n)})$. The removing from stack operation at its worst case is $O(n\log{(n)})$, because you can remove at most $n$ "sections" of the stack, and popping and pushing into a set is logarithmic time. But since you can only remove each "section" of cards once, the total cost of all remove operations is at most log-linear. The inserting from stack operation is logarithmic time, also due to popping and pushing into a set.

https://open.kattis.com/problems/majoritycard
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

struct comp_pair {
    template <class T1, class T2>
    bool operator()(const pair<T1, T2>& a, const pair<T1, T2>& b) const {
        if (a.first == b.first) return a.second < b.second;
        return a.first > b.first;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    umap<int, int> freq;
    set<ii, comp_pair> maj;
    deque<ii> stack;

    string s;
    int x, y, z;
    while (n--) {
        cin >> s;

        if (s == "PUT_TOP") {
            cin >> x >> y;
            stack.push_front({x, y});
            maj.erase({freq[y], y});
            freq[y] += x;
            maj.insert({freq[y], y});
        } else if (s == "PUT_BOTTOM") {
            cin >> x >> y;
            stack.push_back({x, y});
            maj.erase({freq[y], y});
            freq[y] += x;
            maj.insert({freq[y], y});
        } else if (s == "REMOVE_TOP") {
            cin >> z;
            while (z) {
                auto itr = stack.begin();
                maj.erase({freq[itr->second], itr->second});
                int diff = min(itr->first, z);
                itr->first -= diff;
                freq[itr->second] -= diff;
                maj.insert({freq[itr->second], itr->second});
                if (itr->first == 0) stack.pop_front();
                z -= diff;
            }
        } else {
            cin >> z;
            while (z) {
                auto itr = stack.rbegin();
                maj.erase({freq[itr->second], itr->second});
                int diff = min(itr->first, z);
                itr->first -= diff;
                freq[itr->second] -= diff;
                maj.insert({freq[itr->second], itr->second});
                if (itr->first == 0) stack.pop_back();
                z -= diff;
            }
        }

        cout << maj.begin()->second << '\n';
    }
}
```
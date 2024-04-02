---
tags:
  - competitive-programming/catalog/kattis
name: Distributing Ballot Boxes
---
#competitive-programming/greedy
#competitive-programming/ds/priority-queue
## _Solution:_
Concept: Start with one ballot box per city. Greedily give the city with the largest person per box the next ballot box. Do this until you run out of boxes.

Use a priority queue to keep track of number of people and boxes in the city, and have a comparator that calculates the maximum number of people per box.

https://open.kattis.com/problems/ballotboxes
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
        int na = a.first / a.second + (a.first % a.second != 0);
        int nb = b.first / b.second + (b.first % b.second != 0);
        return na < nb;
    }
};

int n, k;
priority_queue<ii, vii, comp_pair> q;

int solve() {
    while (k--) {
        ii c = q.top(); q.pop();
        c.second++;
        q.push(c);
    }
    
    int a = q.top().first, b = q.top().second;
    return a / b + (a % b != 0);
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    while (cin >> n >> k && n != -1 && k != -1) {
        q = priority_queue<ii, vii, comp_pair>();
        k -= n;
        while (n--) {
            int a;
            cin >> a;
            q.push({a, 1});
        }

        cout << solve() << '\n';
    }
}
```
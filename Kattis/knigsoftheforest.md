---
tags:
  - competitive-programming/judges/kattis
name: Knigs of the Forest
date: 2023-09-11
---
#competitive-programming/simulation
#competitive-programming/ds/priority-queue
## _Solution:_
Simulate finding the maximum strength moose. Use priority queue to keep track of maximum. If moose is Karl within $n$ years, then print year.

https://open.kattis.com/problems/knigsoftheforest
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
        return a.first < b.first;
    }
};

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int k, n;
    cin >> k >> n;

    priority_queue<ii, vii, comp_pair> q;
    vii next(n + 1);
    int y, p;
    cin >> y >> p;
    y -= 2011;
    
    if (y == 0) {
        q.push({p, 1});
    } else {
        next[y] = {p, 1};
    }

    f (i, 0, n + k - 2) {
        cin >> y >> p;
        y -= 2011;
        if (y == 0) {
            q.push({p, 0});
        } else {
            next[y] = {p, 0};
        }
    }

    f (i, 0, n) {
        ii c = q.top(); q.pop();
        if (c.second) {
            cout << (2011 + i);
            return 0;
        }
        q.push(next[i + 1]);
    }
    cout << "unknown";
}
```
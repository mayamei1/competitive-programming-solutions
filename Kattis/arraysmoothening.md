---
tags:
  - competitive-programming/catalog/kattis
name: Array Smoothening
---
#competitive-programming/greedy
#competitive-programming/ds/priority-queue
## _Solution:_
Concept: Greedily decrement from most frequent.

Count up frequency of occurrences with a hash map. Take all frequencies and put it into a priority queue. Pop top value, decrement, and push back into p-queue. Do this $k$ times.

https://open.kattis.com/problems/arraysmoothening
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

priority_queue<int, vi> q;
int n, k;
int solve() {
    while (k--) {
        int c = q.top(); q.pop();
        q.push(c-1);
    }
    return q.top();
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n >> k;

    umap<int, int> freq;
    f (i, 0, n) {
        int a;
        cin >> a;
        freq[a]++;
    }

    for (ii f : freq) {
        q.push(f.second);
    }

    cout << solve();
}
```
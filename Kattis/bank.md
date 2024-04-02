---
tags:
  - competitive-programming/catalog/kattis
name: Bank Queue
---
#competitive-programming/greedy #competitive-programming/ds/priority-queue 
## _Solution:_
Keep a priority queue of people to keep, where the person with the lowest amount of cash is at the top of the heap. Iterate through each time step. At each step $t$ (starting at $t=1$), there should be $t$ people in the priority queue. If there are not $t$ people, fill it out with the people who would leave at time $t$. Once it is full, start trying to remove people from the priority queue to be replaced by people who will leave at time $t$ and also have more money. 

https://open.kattis.com/problems/bank
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

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, t;
    cin >> n >> t;

    vii e;
    f (i, 0, n) {
        int ci, ti;
        cin >> ci >> ti;
        e.push_back({ti, ci});
    }

    sort(e.begin(), e.end());

    int c = 0;
    int ans = 0;
    priority_queue<int, vi, greater<int>> pq;
    f (i, 0, t) {
        while (c != n && e[c].first == i) {
            if (pq.size() <= i) pq.push(e[c].second);
            else {
                int tmp = pq.top(); pq.pop();
                pq.push(max(tmp, e[c].second));
            }
            c++;
        }
    }
    while (!pq.empty()) {
        ans += pq.top(); pq.pop();
    }
    cout << ans;
}
```
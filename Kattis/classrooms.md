---
tags:
  - competitive-programming/catalog/kattis
name: Classrooms
---
#competitive-programming/greedy #competitive-programming/ds/multiset 
## _Solution:_
Sort in ascending order of termination time (then in ascending order of starting time). Keep a multiset of $k$ termination times. For each event, check for classroom with latest termination time that can still allow for the current event. If it exists, then set this classroom's termination time to now be the new event's termination time. If it doesn't exist, then skip adding this event.

https://open.kattis.com/problems/classrooms
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

bool comp(ii& a, ii& b) {
    if (a.second == b.second) return a.first < b.first;
    else return a.second < b.second;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, k;
    cin >> n >> k;

    vii events(n);
    f (i, 0, n) {
        int s, t;
        cin >> s >> t;
        events[i] = {s, t};
    }

    sort(events.begin(), events.end(), comp);

    multiset<int, greater<int>> s;
    f (i, 0, k) s.insert(0);

    int ans = 0;
    for (ii e : events) {
        auto itr = s.upper_bound(e.first);
        if (itr == s.end()) continue;
        s.erase(itr);
        s.insert(e.second);
        ans++;
    }

    cout << ans;
}
```
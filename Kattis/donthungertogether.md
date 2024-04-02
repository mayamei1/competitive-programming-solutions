---
tags:
  - competitive-programming/catalog/kattis
name: Don't Hunger Together
---
#competitive-programming/binary-search
#competitive-programming/simulation
#competitive-programming/ds/priority-queue
## _Solution:_
Binary search possible answers (ignoring number of players until the end), and simulate to check if valid answer. With simulation, keep a priority queue that prioritizes by earliest expiration turn. Possible answers can be decimals, so it may be possible to use `double` data type, but this solution uses 64-bit integer, with a $10^9$ times offset.

https://open.kattis.com/problems/donthungertogether
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

#define id pair<ull,ull>
#define offset 1000000000ull

struct comp_pair {
    template <class T1, class T2>
    bool operator()(const pair<T1, T2>& a, const pair<T1, T2>& b) const {
        return a.second > b.second;
    }
};

ull n, k;
vector<id> qf;
ull ans;

bool check() {
    priority_queue<id, vector<id>, comp_pair> q;
    f (i, 0, n) {
        q.push(qf[i]);
        ull sum = 0;
        while (true) {
            if (q.empty()) return false;
            id c = q.top(); q.pop();
            if (i >= c.second) continue;
            if ((sum + c.first) >= ans) {
                q.push({sum + c.first - ans, c.second});
                break;
            } else {
                sum += c.first;
            }
        }
    }
    return true;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n >> k;
    qf = vector<id>(n);
    f (i, 0, n) {
        cin >> qf[i].first >> qf[i].second;
        qf[i].first *= offset;
    }

    ans = 1;
    
    if (!check()) {
        cout << "-1";
        return 0;
    }

    ull max_ans = 0;
    ull l = 0, h = 1000000000ull * offset;
    while (l <= h) {
        ans = (h - l) / 2 + l;
        if (check()) {
            max_ans = max(max_ans, ans);
            l = ans + 1;
        } else {
            h = ans - 1;
        }
    }

    double d_ans = (double)max_ans / offset / k;
    printf("%0.32lf", d_ans);
}
```
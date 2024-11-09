---
tags:
  - competitive-programming/judges/kattis
name: Continuous Median
date: 2022-10-17
---
#competitive-programming/simulation #competitive-programming/ds
## _Solution:_
Use a multiset and an iterator/pointer to keep track of middle. Be sure to keep track of whether the new value is $<$ or $\ge$ than the current middle (C++ multiset inserts to the right most) and to keep track of even/odd parity to figure out how to move the iterator.

Another way to solve this is to keep track of a max heap for the left side and a min heap for the right side. Median is stored in the heap with the larger size. After selecting which side to insert to, if one side has a size two greater than the other, balance out.

https://open.kattis.com/problems/continuousmedian
```cpp
#include <iostream>
#include <vector>
#include <utility>
#include <string>
#include <tuple>
#include <cmath>
#include <algorithm>
#include <queue>
#include <stack>
#include <unordered_map>
#include <map>
#include <unordered_set>
#include <set>
#include <climits>
#include <limits>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>
#define ll long long int
#define ull unsigned ll

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;

    for (int i = 0; i < t; i++) {
        int n;
        cin >> n;

        ull a_i;
        cin >> a_i;
        multiset<ull> sorted_a;
        sorted_a.insert(a_i);
        multiset<ull>::iterator mid = sorted_a.begin();
        ull sum_median = *mid;
        for (int j = 1; j < n; j++) {
            cin >> a_i;
            sorted_a.insert(a_i);
            if (a_i < *mid && j % 2 == 1) {
                mid--;
            } else if (a_i >= *mid && j % 2 == 0) {
                mid++;
            }

            if (j % 2) {
                sum_median += (*mid + *next(mid)) / 2;
            } else {
                sum_median += *mid;
            }
        }

        cout << sum_median << '\n';
    }
}
```
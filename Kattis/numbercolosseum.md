---
type:
  - competitive-programming
  - kattis
tags:
  - simulation
  - ds/stack
name: Number Colosseum
---
## _Solution:_
Simulate :)

https://open.kattis.com/problems/numbercolosseum
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
#include <map>
#include <set>
#include <limits>

#define ii pair<int, int>
#define vi vector<int>
#define vii vector<ii>
#define vvi vector<vi>
#define vvii vector<vii>

using namespace std;

int main() {
    int n;
    cin >> n;

    stack<int> pos;
    stack<int> neg;
    for (int i = 0; i < n; i++) {
        int temp;
        cin >> temp;

        if (temp > 0) pos.push(temp);
        else neg.push(temp);

        while (!pos.empty() && !neg.empty()) {
            int result = pos.top() + neg.top();
            pos.pop();
            neg.pop();

            if (result > 0) pos.push(result);
            else if (result < 0) neg.push(result);
        }
    }

    if (!pos.empty()) {
        cout << "Positives win!\n";
        vi arr;
        while (!pos.empty()) {
            arr.push_back(pos.top());
            pos.pop();
        }
        for (int i = arr.size() - 1; i >= 0; i--) {
            cout << arr[i] << ' ';
        }
    } else if (!neg.empty()) {
        cout << "Negatives win!\n";
        vi arr;
        while (!neg.empty()) {
            arr.push_back(neg.top());
            neg.pop();
        }
        for (int i = arr.size() - 1; i >= 0; i--) {
            cout << arr[i] << ' ';
        }
    } else {
        cout << "Tie!";
    }
}
```
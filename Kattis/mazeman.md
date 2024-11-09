---
tags:
  - competitive-programming/judges/kattis
name: MazeMan
date: 2023-04-17
---
#competitive-programming/graph/flood-fill
#competitive-programming/graph/bfs
## _Solution:_
Flood fill starting from each letter and check that it reaches at least one dot.

https://open.kattis.com/problems/mazeman
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
#include <bitset>

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

    int n, m;
    cin >> n >> m;

    vi dr = {-1, 1, 0, 0};
    vi dc = {0, 0, -1, 1};

    vector<string> grid(n);
    vii starts;
    getline(cin, grid[0]);
    for (int i = 0; i < n; i++) {
        getline(cin, grid[i]);

        for (int j = 0; j < m; j++) {
            if ('A' <= grid[i][j] && grid[i][j] <= 'W') {
                starts.push_back({i, j});
            }
        }
    }

    vvi visited(n, vi(m));
    int count = 0;
    for (ii& s : starts) {
        if (visited[s.first][s.second]) continue;

        bool useful = false;
        queue<ii> q;
        
        if (s.first == 0) q.push({s.first + 1, s.second});
        else if (s.first == (n - 1)) q.push({s.first - 1, s.second});
        else if (s.second == 0) q.push({s.first, s.second + 1});
        else q.push({s.first, s.second - 1});

        while (!q.empty()) {
            ii curr = q.front();
            q.pop();

            if (curr.first < 0 || curr.first >= n) continue;
            if (curr.second < 0 || curr.second >= m) continue;
            if (visited[curr.first][curr.second]) continue;

            visited[curr.first][curr.second] = true;
            if ('A' <= grid[curr.first][curr.second] && grid[curr.first][curr.second] <= 'X') continue;
            if (grid[curr.first][curr.second] == '.') useful = true;

            for (int i = 0; i < 4; i++) {
                q.push({curr.first + dr[i], curr.second + dc[i]});
            }
        }

        if (useful) count++;
    }

    int dots = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (!visited[i][j] && grid[i][j] == '.') dots++;
        }
    }

    cout << count << ' ' << dots;
}
```
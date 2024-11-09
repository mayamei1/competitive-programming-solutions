---
tags:
  - competitive-programming/judges/kattis
name: Shotcube
date: 2023-09-12
---
#competitive-programming/complete-search
#competitive-programming/work-backwards
#competitive-programming/graph/bfs
#competitive-programming/bitmask
## _Solution:_
Pre-calculate the distance of each state with BFS. Start the BFS with the "end state," and make valid moves to the next states. Keep track of all of the distances of each state to an end state in an hash map. Then go through each query and print the pre-calculated distance or $-1$ if not valid.

Starting with the BFS with the queries is too slow.

https://open.kattis.com/problems/shotcube
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

int t;
ll st;
umap<ll, int> dist;
queue<pair<ll, int>> q;

void set_(ll& g, int x, int y, bool val) {
    if (val) g |= (1ll << (7 * y + x));
    else g &= ~(1ll << (7 * y + x));
}

bool get_(ll& g, int x, int y) {
    return (g >> (7 * y + x)) & 1ll;
}

void print_g(ll g) {
    f (i, 0, 7) {
        f (j, 0, 7) {
            cout << get_(g, j, i);
        }
        cout << '\n';
    }
}

ll h_flip(ll g) {
    ll a = 0;
    f (i, 0, 7) {
        f (j, 0, 7) {
            set_(a, 6 - j, i, get_(g, j, i));
        }
    }
    return a;
}

ll v_flip(ll g) {
    ll a = 0;
    f (i, 0, 7) {
        f (j, 0, 7) {
            set_(a, j, 6 - i, get_(g, j, i));
        }
    }
    return a;
}

ll d_flip(ll g) {
    ll a = 0;
    f (i, 0, 7) {
        f (j, 0, 7) {
            set_(a, i, j, get_(g, j, i));
        }
    }
    return a;
}

void p_up(ll c, int d, int dir) {
    f (j, 0, 7) {
        int s, e;
        for (s = 0; s < 7 && !get_(c, j, s); s++);
        if (s == 0 && s == 7) continue;
        for (e = s + 1; e < 7 && get_(c, j, e); e++);
        int dmax = e - s;
        
        cf (dd, 1, dmax - 1) {
            ll nc = c;
            f (k, s, s + dd) set_(nc, j, k, 0);
            f (k, 0, dd) set_(nc, j, k, 1);

            if (dir == 0) q.push({nc, d + 1});
            else if (dir == 1) q.push({v_flip(nc), d + 1});
            else if (dir == 2) q.push({d_flip(nc), d + 1});
            else if (dir == 3) q.push({d_flip(v_flip(nc)), d + 1});
        }
    }
}

void precalc() {
    ll a;
    f (i, 0, 5) {
        f (j, 0, 5) {
            a = 0;
            f (k, i, i + 3) {
                f (l, j, j + 3) {
                    set_(a, l, k, 1);
                }
            }
            q.push({a, 0});
            // print_g(a);
            // cout << endl;
        }
    }

    while (!q.empty()) {
        pair<ll,int> pc = q.front(); q.pop();
        ll c = pc.first;
        ll d = pc.second;

        if (dist.find(c) != dist.end()) continue;
        dist[c] = d;

        // print_g(c);
        // cout << d << endl;
        // int aa;
        // cin >> aa;

        ll dc = v_flip(c);
        ll lc = d_flip(c);
        ll rc = v_flip(lc);
        p_up(c, d, 0);
        p_up(dc, d, 1);
        p_up(lc, d, 2);
        p_up(rc, d, 3);
    }
}

int solve() {
    if (dist.find(st) == dist.end()) return -1;
    else return dist[st];
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    precalc();

    cin >> t;
    while (t--) {
        string s;
        st = 0;

        f (i, 0, 7) {
            cin >> s;
            f (j, 0, 7) {
                set_(st, j, i, s[j] == 'X');
            }
        }

        cout << solve() << '\n';
    }
}
```
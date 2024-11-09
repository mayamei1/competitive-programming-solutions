---
tags:
  - competitive-programming/judges/kattis
name: A Multiplication Game
date: 2020-02-25
---
#competitive-programming/greedy #competitive-programming/math #competitive-programming/dp/recursive 
## _Solution:_
**Sub-$O(n)$ solution**
Try every possible move, and memoize the result for any given number.

**$O(\log n)$ solution**
Observe that whoever wins is based on parities of powers of $18$. For example, anything $1\leq n\leq1\times9$ Stan wins, and anything $1\times9<n\leq1\times18$ Ollie wins. Anything $18<n\leq18\times9$ Stan wins, while Ollie wins $18\times9<n\leq18\times18$. This is to say that you want to be in the same half of the parity as $n$ to win. If you are not in the correct half, any attempts to switch halves can easily be thwarted. If you do a $2$, the other will do a $9$. If you do a $9$, the other will do a $2$. Any other in between number has a way for the other person to keep their side of the parity.

Divide $18$ and round up until you get a value $x\leq18$. If $x\leq9$ Stan wins, else Ollie wins.

**$O(1)$ solution**
Use floating point math to do log base $18$. Does come with the potential issue of floating point error.

https://open.kattis.com/problems/amultiplicationgame
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

    ll n;
    

    while (cin >> n) {
        while (n > 18) {
            n = (n + 17) / 18;
        }

        if (n <= 9) cout << "Stan wins." << endl;
        else cout << "Ollie wins." << endl;
    }
}
```
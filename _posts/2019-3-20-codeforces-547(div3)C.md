---
layout: post
title: '[Codeforces] Round547(div3) : C - Polycarp Restores Permutation'
---

[Round547(div3) : C - Polycarp Restores Permutation](http://codeforces.com/contest/1141/problem/C)

## 풀이

수학

O(n^2)으로 x값을 한바퀴돌면서 순열이 성립하는지 한바퀴 체크하면 쉽겠지만,

n의 범위가 200000까지라서 시간초과가 난다.

키포인트는 q[i]를 누적해서 더했을때 최소값 + 1 이 초항(x)가 되야된다는것이다.(항상 1부터 시작하니까)

초항(x)값을 계산했으면, chk배열로 중복체크를 하면서 x+누적합q[i]이 1부터 n까지 사이에 존재하는지만 체크하면 된다.

## 코드

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <queue>
using namespace std;

long long q[200001];
int chk[200001];
int main() {
    int n;
    cin >> n;
    long long m = 0;
    q[0] = 0;
    for (int i = 1; i < n; i++) {
        int tmp;
        cin >> tmp;
        q[i] = q[i - 1] + tmp;
        if (q[i] < m) {
            m = q[i];
        }
    }
    long long x = 1 - m;
    vector<int> v;
    int flag = 0;
    for (int i = 0; i < n; i++) {
        int num = x + q[i];
        if (chk[num] == 0 && num>=0 && num<=n) {
            chk[num] = 1;
            v.push_back(num);
        }
        else {
            flag = 1;
            break;
        }
    }
    if (flag) {
        cout << -1;
    }
    else {
        for (auto x : v) {
            cout << x << ' ';
        }
    }
    return 0;
}
```

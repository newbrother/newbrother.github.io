---
layout: post
title: '[Codeforces] Round574(div2) : A - Drinks Choosing'
---

[Round574(div2) : A - Drinks Choosing](http://codeforces.com/contest/1195/problem/A)

## 풀이

브루투포스

총 k가지 경우만 있다고 했으므로 메모이제이션할 배열을 만들고,

2명이 차면 세트가 되므로, 2쌍이 된 세트의 숫자를 기록해둔다.

총세트는 n/2를 반올림한수만큼 주어진다고 했으므로,

완성된세트수(num)*2 + 총세트-완성세트수(혼자있는세트)를 더한값이 정답이 된다.

## 코드

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>
#include <cstring>
#include <string>
#include <queue>
#include <map>
using namespace std;
 
int match[1001];
 
int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    
    int n, k;
    cin >> n >> k;
    int sets = (n + 1) / 2;
    int num = 0;
    int tmp;
    for (int i = 0; i < n; i++) {
        cin >> tmp;
        if (match[tmp] == 1) {
            num++;
            match[tmp] = 0;
        }
        else {
            match[tmp] = 1;
        }
    }
    cout << sets-num + num*2;
    return 0;
}
```

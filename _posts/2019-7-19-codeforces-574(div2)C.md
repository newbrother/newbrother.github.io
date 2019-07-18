---
layout: post
title: '[Codeforces] Round574(div2) : C - Basketball Exercise'
---

[Round574(div2) : C - Basketball Exercise](http://codeforces.com/contest/1195/problem/C)

## 풀이

DP

백준DP문제중 포도주문제와 비슷했어서 아이디어가 바로 떠올랐다.

이 DP의 포인트는 중간에 한번 선택을 안해도 된다는것이다.

중간에 한번 선택을 안하는 대신, 그전의 두값중 큰값을 기록해두면 된다.

그리고는 다음과 같은 지그재그로 max를 구하거나 선택안하는 경우를 점화식을 세우면 된다. 

```cpp
dp2[i] = max(dp[i - 1],dp3[i-1]) + arr2[i];
dp[i] = max(dp2[i - 1],dp3[i-1]) + arr[i];
dp3[i] = max(dp[i - 1], dp2[i - 1]);
```

long long 타입으로 dp를 만들지 않아서 한번 틀리는 실수를 했다.

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
 
int arr[100000];
int arr2[100000];
long long dp[100000];
long long dp2[100000];
long long dp3[100000];
int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    for (int i = 0; i < n; i++) {
        cin >> arr2[i];
    }
    dp[0] = arr[0], dp2[0] = arr2[0], dp3[0] = 0;
    for (int i = 1; i < n; i++) {
        dp2[i] = max(dp[i - 1],dp3[i-1]) + arr2[i];
        dp[i] = max(dp2[i - 1],dp3[i-1]) + arr[i];
        dp3[i] = max(dp[i - 1], dp2[i - 1]);
    }
    cout << max(dp[n - 1], dp2[n - 1]);
    return 0;
}
```

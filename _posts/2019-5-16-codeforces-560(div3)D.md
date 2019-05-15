---
layout: post
title: '[Codeforces] Round560(div3) : D - Almost All Divisors'
---

[Round560(div3) : D-Almost All Divisors](http://codeforces.com/contest/1165/problem/D)

## 풀이

브루트포스

언뜻보면 공약수를 모두찾는 간단한 문제같다.

1과 자신을 제외한 모든 공약수가 주어진다고 했으므로,

정렬 한 후에 첫번째항과 마지막항을 곱하면 원래의 수를 구할 수 있다.

하지만 이문제에서는 입력데이터 값이 올바른지 체크를 해야한다.

시간이 없는 상황에서 이부분에서 소수가 아닌지만 체킹을 하고 냈더니 당연히 틀렸고,

구한 수에서 모든 약수를 다시 구해서 비교했더니 시간초과가 났다.

접근은 맞았지만 빠르게 풀 수 있는 해법은 이렇다.

벡터를 만들고 모든 약수를 구해서 넣는다.

양쪽 (i값과, num/i값)을 넣어주면서 i*i까지만 살핀다.(에라토스테네스의 체와 비슷하다)

그리고 주어진 입력벡터와 만든벡터가 동일한지 dd==d 조건을 살피고 맞으면 올바른값을 출력하고,

다르다면 -1을 출력하면 된다.

## 코드

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>
#include <cstring>
#include <string>
#include <queue>
#include <cmath>
using namespace std;

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        vector<long long> d(n);
        for (int i = 0; i < n; i++) {
            cin >> d[i];
        }
        sort(d.begin(), d.end());
        int Min = d[0];
        int Max = d[n - 1];
        long long num = 1LL*Min*Max;
        vector<long long> dd;
        for (int i = 2; 1LL * i*i <= num; i++) {
            if (num%i == 0) {
                dd.push_back(i);
                if (i != num / i) {
                    dd.push_back(num / i);
                }
            }
        }
        sort(dd.begin(),dd.end());
        if (dd == d) {
            cout << num << '\n';
        }
        else {
            cout << -1 << '\n';
        }
    }
    return 0;
}
```

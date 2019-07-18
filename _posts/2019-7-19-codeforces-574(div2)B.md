---
layout: post
title: '[Codeforces] Round574(div2) : B - Sport Mafia'
---

[Round574(div2) : B - Sport Mafia](http://codeforces.com/contest/1195/problem/B)

## 풀이

이분탐색

10억(10^9)까지 살펴봐야하므로

이분탐색을 생각해내야한다. 

(처음에 당연하게도 dfs로 풀었다가 시간초과를 냈다)

이분탐색을 해보자

이때, mid는 사탕을 넣은 횟수이다.

한번넣거나 n번 모두 넣거나 했으니 0부터 n까지 이분탐색한다.

남은 사탕을 뜻하는 long long type인 ret을 1부터 mid까지의 합으로 연산하고,

이값에서 n-mid를 뺀다(n에서 mid를 빼면 사탕 먹은 개수이다)

ret이 k라면 찾은것이다. n-mid(먹은 개수)가 정답이다.



## 코드

```cpp
#include <iostream>
using namespace std;
#define endl '\n'
 
 
int main() {
   ios::sync_with_stdio(false);
   cin.tie(NULL);
   
   int n, k;
   cin >> n >> k;
 
   int low = 0;
   int high = n;
   long long ret = 0;
   while (low <= high) {
      long long mid = (low + high) / 2;
      ret = (mid * (mid + 1)) / 2 - (n - mid);
      if (ret == k) {
         cout<< n - mid <<endl;
         return 0;
      }
      if (ret > k) {
         high = mid - 1;
      }
      else {
         low = mid + 1;
      }
   }
}
```

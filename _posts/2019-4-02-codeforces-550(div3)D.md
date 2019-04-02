---
layout: post
title: '[Codeforces] Round550(div3) : D - Equalize Them All'
---

[Round550(div3) : D - Equalize Them All](http://codeforces.com/contest/1144/problem/D)

## 풀이

Greedy

입력되는 뒤죽박죽 값들을 모두 같은 숫자로 만드는 최소 연산 횟수를 print하고

어느연산(두가지, 뒤idx와 차이를 더하는연산과 빼는연산)을 어떤 인덱스에서 수행했는지 print하는 문제이다.

input이 20만이라 O(n)의 풀이를 생각해내야만 한다.

dp아니면 그리디가 있겠지만 시험시간의 압박으로 contest중에는 과감하게 넘겼다.(E를시도했다가 아쉽게 틀렸다)

(이번대회에서 D푸신분은 정말 많았지만 E푸신분은 거의없었다...=>문제보는 눈을 길러야함)

그리디가 다그렇지만, 튜토리얼을 보니까 약간 허무하면서도 대단했다.

최빈값을 찾고, 'n - 최빈수' 이 바꿔야하는 최소연산횟수이다.

(즉, 최빈값으로 값들을 맞춰주는것이다.)

그 최빈값이 나온 첫idx에서 0까지 idx를 뺴나가면서 arr의 값을 최빈값으로 맞춰주며 print한다.

그리고 i=0에서 n-1까지 가면서 arr의값이 최빈값과 다르다면 최빈값으로 바꿔주며 print한다.

마지막으로 print할때 내가 애먹었던 부분인데, 연산1번(더하는연산)인지 연산2번(빼는연산)인지를

정해줘야한다. 

1아니면 2이니까 , 1 + 조건을 만족하면 1추가 하는식으로 하면 된다.

처음 반복에서는 왼쪽방향으로 가니까 

왼쪽이 더크면 조건을 만족, 1을더한다((arr[i-1]가 최빈값보다 커서 빼줘야한다))

cout<<1+(arr[i-1]>arr[i])

두번째 반복에서는 오른쪽 방향으로 가니까 

오른쪽이 더크면 1을더한다(arr[i+1]가 최빈값보다 커서 빼줘야한다)

cout<<1+(arr[i+1]>arr[i])



## 코드

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <functional>
#include <cstring>
#include <queue>
using namespace std;

int arr[200001];
int cnt[200001];

int main()
{
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>arr[i];
        cnt[arr[i]]++;
    }
    int maxFre=cnt[0];
    int maxIdx=0;
    for(int i=1;i<=200000;i++){
        if(maxFre<cnt[i]){
            maxFre=cnt[i];
            maxIdx=i;
        }
    }
    //cout<<maxFre<<' '<<maxIdx<<'\n';
    int idx=0;
    for(int i=0;i<=200000;i++){
        if(arr[i]==maxIdx){
            idx=i;
            break;
        }
    }
    cout<<n-maxFre<<'\n';
    for(int i=idx;i>0;i--){
            cout<<1+(arr[i-1]>arr[i])<<' '<<i<<' '<<i+1<<'\n';
            arr[i-1]=arr[i];
    }
    for(int i=0;i<n-1;i++){
        if(arr[i+1]!=maxIdx){
            cout<<1+(arr[i+1]>arr[i])<<' '<<i+2<<' '<<i+1<<'\n';
            arr[i+1]=arr[i];
        }
    }
    return 0;
}

```

---
layout: post
title: '[Codility] Lesson4 : MaxCounters'
---

## 풀이

Respectable난이도로 표기된 문제만 올릴예정.

이 문제는 단순히 연산대로 풀이하면 O(N*M)이 되어 시간초과가 난다.

시간복잡도를 줄이는게 관건.

N+1연산이 나올시 lastMax에 당시 Max값을 임시저장한다음 값이 갱신되거나 마지막에 업데이트를 하는 방식으로

O(M+N)으로 시간복잡도를 줄일 수 있었다.

## 코드

```cpp
MaxCounters

int arr[100001];

vector<int> solution(int N, vector<int> &A) {
    vector<int> result;
    //N+1이 나올때 lastmax에 logging하는것으로 시간복잡도 해결.
    int lastMax=0;
    int max=0;
    int size=A.size();
    for(int i=0;i<size;i++){
        if(A[i]==(N+1)){
            lastMax=max;
        }else{
            if(arr[A[i]] < lastMax){
                arr[A[i]] = lastMax;
            }
            arr[A[i]]++;
            if(arr[A[i]] > max){
                max = arr[A[i]];
            }
        }
    }
    //result벡터로 정답을 옮겨주며, 갱신안된 숫자들은 lastMax로 아직 변경안되었으므로 해당작업 수행
    for(int i=1;i<=N;i++){
        if(arr[i] < lastMax){
            result.push_back(lastMax);
        }else{
            result.push_back(arr[i]);
        }
    }
    return result;
}
```

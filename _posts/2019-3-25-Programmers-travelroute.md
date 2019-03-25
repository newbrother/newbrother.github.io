---
layout: post
title: '[Programmers] BFS/DFS : 여행경로'
---

[BFS/DFS : 여행경로](https://programmers.co.kr/learn/courses/30/lessons/43164)

## 풀이

깊이우선탐색(DFS)

[a,b]는 a->b로 방향그래프이다.

a가 ICN(출발점)인 idx들에서 dfs를 시작한다. 해당 idx의 b와 같은 a idx를 또 찾는다.

이런식으로 가능한 경우를 모두 탐색하다가, cnt가 n과 같아지면 모든 경로를 살펴보는데 성공한 것이다.

그때 마지막idx의 b를 경로저장한 배열에 넣어준다음에, 알파벳 경로가 앞서는지 확인을 한다.

(문제조건에 알파벳 경로가 앞서는것을 출력해야한다고 했기때문이다.)

String객체는 알파벳 순서로 비교연산이 되기때문에 기존의 정답과 현재정답의 경로를 비교해서

현재 정답이 적으면 갱신작업을 하면 문제 풀이에 성공한다.

(기차에서 비몽사몽 코딩한거라 dfs함수내 정답갱신하는 부분에서 비효율적인 부분이 조금 있는것같다)


## 코드

```cpp
#include <string>
#include <vector>
#include <cstring>
using namespace std;

vector<string> answer;
vector<string> curA;
int chk[10000];
int ansflag=0;
void dfs(vector<vector<string>> &tickets,int cur, int cnt, int n){
    if(cnt==n){
        curA.push_back(tickets[cur][1]);
        //첫정답이거나, 알파벳순으로 앞서거나하면 갱신
        if(ansflag){
            int okflag=0;
            for(int i=0;i<curA.size();i++){
                if(answer[i]>curA[i]){
                    okflag=1;
                    break;
                }else if(answer[i]<curA[i]){
                    break;
                }
            }
            if(okflag){
                answer.clear();
                for(int i=0;i<curA.size();i++){
                    answer.push_back(curA[i]);
                }
            }
        }
        else{
            //첫정답
            for(int i=0;i<curA.size();i++){
                answer.push_back(curA[i]);
            }
            ansflag=1;
        }
        curA.pop_back();
        return;
    }
    for(int i=0;i<n;i++){
        if(chk[i]==0 && tickets[i][0]==tickets[cur][1]){
            chk[i]=1;
            curA.push_back(tickets[i][0]);
            dfs(tickets,i,cnt+1,n);
            chk[i]=0;
            curA.pop_back();
        }
    }
}

vector<string> solution(vector<vector<string>> tickets) {
    //[a,b]는 a->b로 방향그래프이다.
    for(int i=0;i<tickets.size();i++){
        if(tickets[i][0]=="ICN"){
            memset(chk,0,sizeof(chk));
            curA.clear();
            curA.push_back(tickets[i][0]);
            chk[i]=1;
            dfs(tickets,i,1,tickets.size());
        }
    }
    
    return answer;
}
```

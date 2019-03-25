---
layout: post
title: '[Programmers] BFS/DFS : 단어변환'
---

[완전탐색 : 숫자야구](https://programmers.co.kr/learn/courses/30/lessons/43163)

## 풀이

깊이우선탐색(DFS)


제일먼저 words중에 target이 있는지 확인하고,

거꾸로 target에서 begin을 향해서 dfs탐색을 진행했다.

1글자 뺴고 일치하는 문자들은 재귀적으로 계속 탐색진행되서,

모든글자가 begin과 일치하는 것들을 찾는다. 그중 cnt가 가장 적은것을 출력한다.


(기차에서 비몽사몽 코딩한거라 dfs함수내 비효율적인 부분이 조금 있는것같다)


## 코드

```cpp
#include <string>
#include <vector>
using namespace std;
int chk[50];
int answer = -1;

void dfs(vector<string> &words, string begin, int idx,int cnt){
    string str=words[idx];
    int c=0;
    for(int i=0;i<words[0].size();i++){
        if(str[i]==begin[i]){
                c++;
         }
    }
    if(c==words[0].size()-1){
        if(answer==-1 || answer>cnt){
            answer=cnt;
        }
        return;
    }
    
    for(int i=0;i<words.size();i++){
        if(chk[i]==0){
            int c=0;
            for(int j=0;j<words[0].size();j++){
                if(str[j]==words[i][j]){
                    c++;
                }
            }
            if(c==words[0].size()-1){
                chk[i]=1;
                dfs(words,begin,i,cnt+1);
                chk[i]=0;
            }
        }
    }
}

int solution(string begin, string target, vector<string> words) {
    //words중 target부터시작해서 (없으면 0리턴)
    //1글자 빼고 같은것들로 dfs() 수행한다.
    int startIdx=-1;
    for(int i=0;i<words.size();i++){
        if(target==words[i]){
            startIdx=i;
            break;
        }    
    }
    if(startIdx==-1){
        return 0;
    }
    chk[startIdx]=1;
    dfs(words,begin,startIdx,1);
    return answer;
}
```

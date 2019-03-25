---
layout: post
title: '[Programmers] 완전탐색 : 숫자야구'
---

[완전탐색 : 숫자야구](https://programmers.co.kr/learn/courses/30/lessons/42841)

## 풀이

완전탐색

어떻게하면 효율적으로 계산할 수 있을까 한참 생각하다가 코드가 너무길어져서

그냥 가능한 모든 경우를 배열로 만들어서 했다.

모든 경우를 반복하며 baseball배열의 strike랑 ball의 숫자와 비교해서

틀리면 체크하는 식으로 계산했다.

마지막엔 틀리지않은 숫자만 세주면 된다.


시간복잡도는 9x8x7(504)에 대해서 각각 최대 100번씩만 비교하면되서

50000번 정도만 계산하면 되서 충분하다.


시뮬레이션이나 게임같은 알고리즘에서는
 
모든 배열을 미리만든 후에 전체를 탐색하는 방법이 쉽게 빠르고 풀 수 있는 경우가 많은것 같다.

## 코드

```cpp
#include <string>
#include <vector>
using namespace std;
//시간복잡도:100000(100*1000)
//9x8x7=504
const int maxsize = 504;
int arr[504];
//가능하면0 불가능하면1
int chk[504];

int solution(vector<vector<int>> baseball) {
    int answer = 0;
    int numbers[10] = {0,1,2,3,4,5,6,7,8,9};
    int idx=0;
    for(int i=1;i<=9;i++){
        for(int j=1;j<=9;j++){
            if(i==j)
                continue;
            for(int k=1;k<=9;k++){
                if(k==i || k==j)
                    continue;
                arr[idx++]=100*i+10*j+k;
            }
        }
    }
    for(int j=0;j<maxsize;j++){
            int aa = arr[j]/100;
            int bb = arr[j]/10%10;
            int cc = arr[j]%10;
            for(int i=0;i<baseball.size();i++){
                int a=baseball[i][0]/100;
                int b=baseball[i][0]/10 % 10;
                int c=baseball[i][0]%10;
                int st=baseball[i][1];
                int ball = baseball[i][2];
                int sums=0;
                int sumb=0;
                if(a==aa){
                    sums++;
                }else if(a==bb || a==cc){
                    sumb++;
                }
                if(b==bb){
                    sums++;
                }else if(b==aa || b==cc){
                    sumb++;
                }
                if(c==cc){
                    sums++;
                }else if(c==bb || c==aa){
                    sumb++;
                }
                
                if(sums!=st || sumb!=ball){
                    chk[j]=1;
                    break;
                }
            }
    }
    
    for(int j=0;j<maxsize;j++){
        if(chk[j]==0)
            answer++;
    }
    
    return answer;
}
```

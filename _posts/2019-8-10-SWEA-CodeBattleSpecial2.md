---
layout: post
title: '[SWEA] CodeBattle[레벨업코스] : 2.키조사'
---

## 풀이

삼성역량테스트B형 유형 문제
STL사용금지, API만 구현하는 유형.

해싱 간단하게 구현했다.

소수이런걸 찾아서 하면 더 빠른것 같지만,

무난하게 크게잡고 체이닝 하는 방식으로 구현했다.

## 코드

```cpp
키조사

typedef unsigned long long ulong;
#define M 1000001
int arr[M];
 
struct Node
{
    ulong data;
    Node* next;
};
 
Node nodePool[1500000];
int nodeCnt;
 
struct List
{
    Node* head;
    Node* tail;
    Node* ptr;
 
    void init() {
        head = &nodePool[nodeCnt++];
        tail = head;
        head->next = tail;
        tail->next = tail;
        ptr = head;
    }
    void add(ulong d) {
        Node* temp = &nodePool[nodeCnt++];
        temp->data = d;
        temp->next = ptr->next;
        ptr->next = temp;
        ptr = temp;
    }
};
 
List list[M];
 
void init()
{
    nodeCnt = 0;
    for (register int i = 0; i < M; i++) {
        arr[i] = 0;
    }
    for (register int i = 0; i < M; i++) {
        list[i].init();
    }
}
//나누기십만
//일단 배열 만들고
//arr에 충돌숫자 기록해둠
//만약 충돌숫자가 1이상이면
//해당 
int checkKey(ulong key)
{
    int num = key % M;
    if (arr[num] > 0) {
        //리스트 순회해서 찾아봄
        Node * np = list[num].head;
        int flag = 0;
        for (int i = 0; i < arr[num]; i++) {
            np = np->next;
            if (key == np->data) {
                flag = 1;
                break;
            }
        }
        //겹치는게 존재
        if (flag) {
            return 0;
        }
        //겹치는게 없음
        else {
            arr[num]++;
            list[num].add(key);
            return 1;
        }
    }
    else {
        arr[num] = 1;
        list[num].add(key);
        return 1;
    }
}
```

---
layout: post
title: '[Codility] Lesson4 : MaxCounters'
---

## 풀이

Respectable난이도로 표기된 문제만 올릴예정.

이 문제는 단순히 연산대로 풀이하면 O(N*M)이 되어 시간초과가 난다.

시간복잡도를 줄이는게 관건.

N+1연산이 나올시 lastMax에 당시 Max값을 임시저장한다음 값이 갱신되거나 마지막에 업데이트를 하는 방식으로

O(M, N)으로 시간복잡도를 줄일 수 있었다.

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

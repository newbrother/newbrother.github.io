---
layout: post
title: '[SWEA]코드배틀(레벨업코스) : 1.수열합치기'
---

## 풀이

삼성SW 역량테스트 B형 유형의 문제이다.
STL사용금지에 API를 설계하는 유형이다.

연결리스트를 사용했다. 

이중 연결리스트 직접 구현해서 사용하려니까 정말 어렵더라.


## 코드

```cpp
//#include <iostream>
//using namespace std;
#define MAX_NODE 1000000
 
struct Node
{
    int data;
    Node* prev;
    Node* next;
};
 
Node nodePool[MAX_NODE];
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
        head->prev = head;
        tail->next = tail;
        tail->prev = head;
        ptr = head;
    }
    void add(int d) {
        Node* temp = &nodePool[nodeCnt++];
        temp->data = d;
        ptr->next->prev = temp;
        temp->next = ptr->next;
        ptr->next = temp;
        temp->prev = ptr;
        ptr = temp;
    }
};
 
List list;
 
void init()
{
    nodeCnt = 0;
    list.init();
}
 
void mergenums(int n, int * arr){
    int num = arr[0];
    int idx = 0;
    Node *np = list.head->next;
    //cout << "npdata : "<<np->data << '\n';
    //순회
    //더큰값 위치 반환
    while (1) {
        if (np == list.tail || np->data > num) {
            break;
        }
        //cout << np->data << ' ';
        np = np->next;
        idx++;
    }
    //cout << "idx : " << idx << '\n';
    //cout << np->data << '\n';
 
    //추가
    List newList;
    newList.init();
    for (int i = 0; i < n; i++) {
        newList.add(arr[i]);
    }
    /*
    cout << "newList" << '\n';
    Node * nnp = newList.head->next;
    while (nnp != newList.tail) {
        cout << nnp->data << ' ';
        nnp = nnp->next;
    }
    cout << '\n';
    */
    //갱신
    //np->prev 다음으로 newList의 처음 연결
    //newList의 마지막숫자 다음(next)로 np연결
     
    np->prev->next = newList.head->next;
    newList.head->next->prev = np->prev;
    newList.tail->prev->next = np;
    np->prev = newList.tail->prev;
    /*
    cout << "list : " << '\n';
    nnp = list.head->next;
    while (nnp != list.tail) {
        cout << nnp->data << ' ';
        nnp = nnp->next;
    }
    cout << '\n';
    */
}
 
int findkth(int kth)
{
    if (kth > 0) {
        Node * nnp = list.head;
        while (kth--) {
            nnp = nnp->next;
        }
        return nnp->data;
    }
    else {
        Node * nnp = list.tail;
        while (kth++) {
            nnp = nnp->prev;
        }
        return nnp->data;
    }
    return 0;
}
```

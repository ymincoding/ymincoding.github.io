---
layout: post
title: "[Everyday Programming]매일프로그래밍 #15"
description: >
    링크드 리스트 N번째 노드 제거하기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

[문제]  
링크드 리스트(linked list)의 머리 노드(head node)와 정수 N이 주어지면, 끝에서 N번째 노드(node)를 제거하고 머리 노드(head node)를 리턴하시오.
단, 리스트를 한번만 돌면서 풀어야합니다. N은 리스트 길이보다 크지 않습니다.  

[Question]  
Given a head node of a singly linked list, remove the Nth last element and return the head node.  

예제)  
> Input: 1->2->3->4->5, N=2  
  Output: 1->2->3->5  

> Input: 1->2->3, N=3  
  Output: 2->3  

> Input: 1, N=1  
  Output: null  

[풀이]  
일단 __링크드 리스트(linked list)__ 를 간단하게 만들었다. class를 이용해서 node 숫자와 다음 node를 가리키는 next 포인터를 맴버변수로 가지는 List 클래스이다.  
~~~c++
class List { 
private: 
	int node;
	List* next;
public:
	List() { next = NULL; }
	~List() {}

	void setNode(int num) {	node = num;	}
	int getNode() {	return node; }
	void setNext(List* ptr) { next = ptr; }
	List* getNext() { return next; }
};
~~~  

__단일 링크드 리스트__ 이므로 제일 앞서 __Head__ 를 선언한 후 next 포인터로 노드를 연결해준다.  
__Head__ 는 고정 포인터로 두고, __ListPtr__ 을 선언해서 다음 노드로 이동하며 새로운 노드를 연결한다.  

끝에서 N번째 노드를 제거해야한다. 즉, 앞에서부터 __(노드 전체 갯수) + 1 - N 번째__  노드이다.  
예를 들어 노드가 5개이고 N이 2라면, 앞에서부터 4번째 노드가 뒤에서 2번째 노드와 같다.  

Head부터 노드를 하나씩 출력하며 next로 이동하다가 지우고자 하는 노드 바로 전에 도착했을 경우, <span style="color: var(--highlight-color)"> __다음 노드를 제거하기 전에 현재 가리키고 있는 노드의 next 포인터를 지우고자 하는 노드의 next 포인터로 할당해주어야 한다. 그렇지 않으면 지운 노드 이후의 리스트들은 전부 메모리에는 남아있지만 가리키는 포인터가 없기 때문에 찾을 수 없게 된다.__ </span> 이 과정이 지난 후에 노드를 제거할 수 있다!  
만약 제일 마지막 노드일 경우, 현재 노드의 next를 NULL로 지정해 주고 다음 노드를 제거한다.  
```c++
List* tempPtr;
tempPtr = listPtr->getNext(); // tempPtr: 지우고자 하는 노드, listPtr: 지우고자 하는 것 바로 전 노드
if (tempPtr->getNext() != NULL) {
	listPtr->setNext(listPtr->getNext()->getNext());
	delete tempPtr;
}
else {
	listPtr->setNext(NULL);
	delete tempPtr;
}
```  

전체 코드는 아래와 같이!  
단일 for문이기 때문에 시간복잡도는 O(n)이다.  
```c++
#include <iostream>
using namespace std;

class List { // 링크드리스트 class 선언
private: 
	int node;
	List* next;
public:
	List() { next = NULL; }
	~List() {}

	void setNode(int num) {	node = num;	}
	int getNode() {	return node; }
	void setNext(List* ptr) { next = ptr; }
	List* getNext() { return next; }
};

int main() {
	cout << "Input linked list numbers: ";

	List* head = new List();
	List* listPtr = NULL;
	int listCount = 0;
	do { // 원하는 만큼 입력받기
		int temp;
		cin >> temp;
		
		List* list = new List();
		list->setNode(temp);
		listCount++;

		if (listCount == 1) {
			head->setNext(list);
			listPtr = list;
		}
		else {
			listPtr->setNext(list);
			listPtr = list;
		}
	} while (getc(stdin) == ' ');

	int Nth;
	while (true) { // 범위에 맞는 N이 입력될 때 까지 반복
		cout << "Input N: ";
		cin >> Nth;
		if (Nth > listCount) {
			cout << "N must be smaller than list size. Please try again." << endl;
		}
		else if (Nth <= 0) {
			cout << "N must be bigger than 0. Please try again." << endl;
		}
		else
			break;
	}
	
	int inverseNth = listCount + 1 - Nth; // 앞에서 몇 번째로 바꿔주기
	listPtr = head;
	for (int i = 1; i <= listCount; i++) {
		if (inverseNth == i) {
			List* tempPtr;
			tempPtr = listPtr->getNext(); // tempPtr: 지우고자 하는 노드, listPtr: 지우고자 하는 것 바로 전 노드
			if (tempPtr->getNext() != NULL) {
				listPtr->setNext(listPtr->getNext()->getNext());
				delete tempPtr;
			}
			else {
				listPtr->setNext(NULL);
				delete tempPtr;
			}
		}
		else {
			cout << listPtr->getNext()->getNode() << " ";
			listPtr = listPtr->getNext();
		}
	}
	if (listCount == 1) { // list가 1개였을 경우 남아있는 것이 없으므로
		cout << "null";
	}
	cout << endl;

	system("pause");
	return 0;
}
```  

*문제 출처 - 2019매일프로그래밍*
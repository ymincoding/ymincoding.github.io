---
layout: post
title: "[Everyday Programming]매일프로그래밍 #16"
description: >
    두 리스트를 합친 정렬된 링크드 리스트(Linked list)
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

[문제]  
두개의 정렬된(sorted) 정수 링크드리스트(linked list)가 주어지면, 두 리스트를 합친 정렬된 링크드리스트를 만드시오.  

[Question]  
Given two sorted integer linked lists, merge the two linked lists. Merged linked list must also be sorted.  

예제)  
> Input: 1->2->3, 1->2->3  
  Output: 1->1->2->2->3->3

> Input: 1->3->5->6, 2->4  
  Output: 1->2->3->4->5->6

[풀이]  
이번에도 list를 구현해볼까 하다가, stl 활용도 연습할 겸 list stl을 처음으로 써보았다.  
list를 구현하는 일이 빠졌으니 내가 해야 할 일은 __정렬된 list를 만드는 것과 두 list를 합치는 것__ 이다.  

stl연습도 할 겸, 원하는 만큼 정수를 입력받으면 정렬된 list로 저장하는 방법을 썼다.  
또한 정렬된 list를 두 개 입력받아야 하니, list를 따로 2개 정의하는 것이 아니라 배열을 이용했다.
~~~c++
#include <list> // stl list 헤더파일

list<int> List[2]; // list 2개
~~~  

정수를 입력받고 list에 저장할 때, iterator를 통해 list 노드에 각각 접근하며 새로 입력받은 정수와 크기를 비교한다. 오름차순으로 정렬하였으며, 입력받은 정수보다 노드의 값이 더 크면 그 위치에 __insert()__ 함수를 사용하여 새로운 노드를 삽입한다.
~~~c++
if (List[count].size() == 0) {
	List[count].push_back(temp);
}
else {
	list<int>::iterator iter;
	iter = List[count].begin();
	for (int i = 0; i < List[count].size(); i++) {
		if (*iter > temp) {
			List[count].insert(iter, temp);
			break;
		}
		else {
			iter++;
		}
	}
	if (iter == List[count].end()) {
		List[count].push_back(temp);
	}
}
~~~  

정렬된 두 list를 하나로 합쳐야한다.  
새로운 orderedList를 선언하고, 두 list에 하나씩 접근하며 크기를 비교하고 더 작은 것 부터 저장한다. while문으로, 두 list의 iterator가 모두 end()와 같아지면 반복문을 끝낸다.  
~~~c++
list<int>::iterator list1 = List[0].begin();
list<int>::iterator list2 = List[1].begin();

list<int> orderedList;
while (1) {
	if (list1 != List[0].end() && list2 != List[1].end()) { // 두 list 다 남아있을 경우
		if (*list1 > *list2) {
				orderedList.push_back(*list2);
				list2++;
		}
		else {
				orderedList.push_back(*list1);
				list1++;
		}
	}
	else if (list1 == List[0].end() && list2 != List[1].end()) { // list2만 남았을 경우
			orderedList.push_back(*list2);
			list2++;
	}
	else if (list2 == List[1].end() && list1 != List[0].end()) { // list1만 남았을 경우
			orderedList.push_back(*list1);
			list1++;
	}
	else { // 두 list 다 끝났을 경우
			break;
	}
}
~~~  

두 개의 list를 입력받을 때, 코드의 반복을 피하기 위해 이중for문을 사용하긴 했지만 이를 제외한다면 시간 복잡도는 O(n)이다.  
알고리즘 연습이 목적인만큼 구현된 stl을 활용하는 것도 중요한 것 같은데 너무 오랜만에 공부를 시작해서 까먹은 부분도 많다🤣  

전체 코드는 아래와 같이!  
~~~c++
#include <iostream>
#include <list>
using namespace std;

int main() {
	list<int> List[2]; // list 2개
	for (int count = 0; count < 2; count++) {
		cout << "Input list" << count + 1 << ": ";
		do { // list 입력받으면서 정렬하기
			int temp;
			cin >> temp;

			if (List[count].size() == 0) {
				List[count].push_back(temp);
			}
			else {
				list<int>::iterator iter;
				iter = List[count].begin();
				for (int i = 0; i < List[count].size(); i++) {
					if (*iter > temp) {
						List[count].insert(iter, temp);
						break;
					}
					else {
						iter++;
					}
				}
				if (iter == List[count].end()) {
					List[count].push_back(temp);
				}
			}

		} while (getc(stdin) == ' ');
	}
	
	list<int>::iterator list1 = List[0].begin();
	list<int>::iterator list2 = List[1].begin();

	list<int> orderedList;
	while (1) {
		if (list1 != List[0].end() && list2 != List[1].end()) { // 두 list 다 남아있을 경우
			if (*list1 > *list2) {
				orderedList.push_back(*list2);
				list2++;
			}
			else {
				orderedList.push_back(*list1);
				list1++;
			}
		}
		else if (list1 == List[0].end() && list2 != List[1].end()) { // list2만 남았을 경우
			orderedList.push_back(*list2);
			list2++;
		}
		else if (list2 == List[1].end() && list1 != List[0].end()) { // list1만 남았을 경우
			orderedList.push_back(*list1);
			list1++;
		}
		else { // 두 list 다 끝났을 경우
			break;
		}
	}

	list<int>::iterator printiter = orderedList.begin();
	for (int i = 0; i < orderedList.size(); i++) {
		cout << *printiter << " ";
		printiter++;
	}
	cout << endl;

	system("pause");
	return 0;
}
~~~  

*문제 출처 - 2019매일프로그래밍*
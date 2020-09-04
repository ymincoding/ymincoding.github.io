---
layout: post
title: "[Everyday Programming]매일프로그래밍 #22"
description: >  
    정렬된 배열에서 정수 탐색하기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

❓__문제__❓  
정렬(sort)된 정수 배열과 정수 n이 주어지면, 배열안에 n이 있는지 체크하시오. 시간복잡도를 최대한 최적화하시오.  

<br/>

❓__Question__❓  
Given a sorted integer array and an integer N, check if N exists in the array.  

<br/>
예제)  

> Input: [1, 2, 3, 7, 10], 7  
  Output: true  
  Input: [-5, -3, 0, 1], 0  
  Output: true  
  Input: [1, 4, 5, 6, 8, 9], 10  
  Output: false  

* * *

❗__풀이__❗  
정수 배열의 처음부터 끝까지 탐색해도 되지만, 만약 찾고자 하는 값이 제일 끝에 있다면 시간 복잡도는 최악의 경우 O(n)이 된다.  
시간복잡도를 최적화하기 위해, __이분검색 알고리즘__ 을 활용하자.  
배열을 계속해서 반으로 나누어서 탐색하기 때문에, 시간 복잡도는 O(log N)이다.  

전체 코드는 아래와 같이!  
~~~c++
#include <iostream>
#include <vector>
using namespace std;

int main() {
	vector<int> inputArray;
	cout << "Input sorted array: ";
	do {
		int temp;
		cin >> temp;
		inputArray.push_back(temp);
	} while (getc(stdin) == ' ');

	// 정렬된 배열의 탐색 알고리즘 - 이분검색
	cout << "Input key number you want to find: ";
	int key;
	cin >> key;

	int mid = inputArray.size() / 2;
	int low = 0; int high = inputArray.size() - 1;
	int resultIndex = -1; // key값이 담긴 index를 저장할 변수 -> 끝까지 찾지 못하면 -1
	while (low <= high)
	{
		if (key > inputArray[mid]) { // key가 중간보다 크면
			low = mid + 1;
		}
		else if (key < inputArray[mid]) { // key가 중간보다 작으면
			high = mid - 1;
		}
		else { // 중간이 key값이면
			resultIndex = mid;
			break;
		}
		mid = (low + high) / 2;
	}

	if (resultIndex == -1) { // 배열에서 찾지 못한경우
		cout << "Output: false" << endl;
	}
	else {
		cout << "Output: true" << endl;
		cout << "Index: " << resultIndex << endl;
	}

	system("pause");
	return 0;
}
~~~  

*문제 출처 - 2019매일프로그래밍*
---
layout: post
title: "[Everyday Programming]매일프로그래밍 #13"
description: >
    N번째 큰 배열 원소 찾기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

[문제]  
정수 배열(int array)과 정수 N이 주어지면, N번째로 큰 배열 원소를 찾으시오.  

[Question]  
Given an integer array and integer N, find the Nth largest element in the array.  

예제)  
> Input: [-1, 3, -1, 5, 4], 2  
  Output: 4

> Input: [2, 4, -2, -3, 8], 1  
  Output: 8

> Input: [-5, -3, 1], 3  
  Output: -5

[풀이]
제일 쉽고 깔끔한 방법을 찾았다.  
vector에 입력받은 배열을 저장하고, __stl sort()__ 를 이용하는 것이다.  
sort()는 __algorithm__ 헤더파일을 include해야한다.  
파라미터로는 벡터의 시작과 끝을 넣어주면 된다.
~~~C++
sort(vector.begin(), vector.end()); // 정렬 (오름차순 기본)
~~~

전체 코드는 아래와 같이!  
~~~c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	vector<int> inputArr;
	cout << "Input an integer array: ";

	do { // 원하는 만큼 배열 입력받기
		int temp;
		cin >> temp;
		inputArr.push_back(temp);
	} while (getc(stdin) == ' ');

	int N;
	cout << "Input an integer N: "; 
	cin >> N;
	if (N > inputArr.size()) {
		cout << "You wrote a wrong number. Please try again." << endl;
		system("pause");
		return 0;
	}

	sort(inputArr.begin(), inputArr.end()); // 정렬 (오름차순 기본)
	cout << "Output: " << inputArr[inputArr.size() - N] << endl;

	system("pause");
	return 0;
}
~~~

*문제 출처 - 2019매일프로그래밍*
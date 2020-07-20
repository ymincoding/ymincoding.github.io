---
layout: post
title: "[Everyday Programming]매일프로그래밍 #21"
description: >  
    2차원 배열 처음부터 모든 원소 방문 후에 다시 돌아오기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

❓__문제__❓  
O(n log n)시간 복잡도를 가진 정수 배열 정렬 알고리즘을 구현하시오.  

<br/>

❓__Question__❓  
Implement an O(n log n) time complexity sorting algorithm.  

<br/>
예제)  

> Input: [3, 1, 5, 6]  
  Output: [1, 3, 5, 6]  

* * *

❗__풀이__❗  
시간 복잡도가 O(n log n)인 정렬 알고리즘은 바로 __합병 정렬(Merge Sort)__ 이다.  
합병 정렬은, 전체 원소를 최소의 단위로 분할하고, 분할한 원소들을 다시 정렬하여 병합하는 방식이다.  

<br/>  

전체 코드는 아래와 같이!  
~~~c++  
#include <iostream>
#include <vector>
using namespace std;

void mergeSort(vector<int> &inputA, int left, int right);

int main() {
	vector<int> inputArray;

	cout << "Input array: ";
	do {
		int temp;
		cin >> temp;
		inputArray.push_back(temp);
	} while (getc(stdin) == ' ');

	// 시간복잡도 O(n log n) -> 합병 정렬
	mergeSort(inputArray, 0, inputArray.size() - 1);

	cout << "Output: ";
	for (int i = 0; i < inputArray.size(); i++) {
		cout << inputArray[i] << " ";
	}
	cout << endl;

	system("pause");
	return 0;
}

void merge(vector<int> &inputA, int left, int mid, int right) {
	vector<int> leftArray;
	for (int a = left; a <= mid; a++) {
		leftArray.push_back(inputA[a]);
	}

	vector<int> rightArray;
	for (int b = mid + 1; b <= right; b++) {
		rightArray.push_back(inputA[b]);
	}

	int i = 0, j = 0, k = left;
	int leftL = mid - left + 1;
	int rightL = right - mid;

	while (i < leftL && j < rightL) {
		if (leftArray[i] < rightArray[j]) {
			inputA[k] = leftArray[i++];
		}
		else {
			inputA[k] = rightArray[j++];
		}
		k++;
	}

	while (i < leftL) {
		inputA[k++] = leftArray[i++];
	}

	while (j < rightL) {
		inputA[k++] = rightArray[j++];
	}

	return;
}

void mergeSort(vector<int> &inputA, int left, int right) {
	if (left < right) {
		int mid = (left + right) / 2;

		mergeSort(inputA, left, mid);
		mergeSort(inputA, mid + 1, right);
		merge(inputA, left, mid, right);
	}

	return;
}
~~~

*합병 정렬 알고리즘 - https://mygumi.tistory.com/309 참조*
*문제 출처 - 2019매일프로그래밍*
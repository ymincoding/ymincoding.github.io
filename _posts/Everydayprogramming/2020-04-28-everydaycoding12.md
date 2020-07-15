---
layout: post
title: "[Everyday Programming]매일프로그래밍 #12"
description: >
    배열에서 자신을 제외한 나머지 요소들의 곱
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

❓__문제__❓  
정수로된 배열이 주어지면, 각 원소가 자신을 뺀 나머지 원소들의 곱셈이 되게하라.
단, 나누기 사용 금지, O(n) 시간복잡도

<br/>

❓__Question__❓  
Given an integer array, make each element a product of all element values without itself.

<br/>

예제)
> input: [1, 2, 3, 4, 5]  
  output: [120, 60, 40, 30, 24]  
  
* * *

❗__풀이__❗  
나누기를 이용하면 정말 쉽게 풀겠지만, 나누기는 사용 금지.  
그 다음 쉬운 방법은 이중for문으로 자신을 제외한 나머지를 곱하는 것이지만 시간복잡도가 O(n^2)가 되므로 금지.  

그 다음은 오래 고민해보았지만 쉽게 답이 나오지 않아 다른 사람들의 풀이를 참고했다.  

__[a, b, c, d]__ 를 입력받았다고 가정했을 때 원하는 결과는 __[bcd, acd, abd, abc]__ 이다.
이를 풀어서 써보면  
<span style="color: #ED908C">1</span> <span style="color: #A1CEAB">b c d</span>  
<span style="color: #ED908C">a </span>  <span style="color: #A1CEAB"> c d</span>  
<span style="color: #ED908C">a b </span>  <span style="color: #A1CEAB"> d</span>  
<span style="color: #ED908C">a b c</span> <span style="color: #A1CEAB">1</span>  
이렇게 나누어진다.  
이렇게 배열을 2개 만들어서 곱해주면 O(n)으로 풀 수 있다.

~~~c++
#include <iostream>
#include <vector>
using namespace std;

int main() {
	vector<int> inputArr; // 원본
	cout << "Input array: ";
	do { // 원하는 만큼의 정수 vector에 넣어주기
		int temp;
		cin >> temp;
		inputArr.push_back(temp);
	} while (getc(stdin) == ' ');
	// ex) input: a b c d

	int* preArr = new int[inputArr.size()];
	int* afterArr = new int[inputArr.size()];

	preArr[0] = 1; 
	for (int i = 1; i < inputArr.size(); i++) {
		preArr[i] = preArr[i - 1] * inputArr[i - 1];
	} // preArr: 1 a ab abc

	afterArr[inputArr.size() - 1] = 1;
	for (int i = inputArr.size() - 2; i >= 0; i--) {
		afterArr[i] = afterArr[i + 1] * inputArr[i + 1];
	} // afterArr: bcd cd d 1

	// 두 배열을 곱하기
	cout << "Output: ";
	for (int i = 0; i < inputArr.size(); i++) {
		cout << preArr[i] * afterArr[i] << " ";
	} // Output: bcd acd abd abc
	cout << endl;

	system("pause");
	return 0;
}
~~~

*풀이 참고: https://cornswrold.tistory.com/62*  
*문제 출처 - 2019매일프로그래밍*
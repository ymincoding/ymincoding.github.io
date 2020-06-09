---
layout: post
title: "[Everyday Programming]매일프로그래밍 #14"
description: >
    제일 긴 공통 접두사(prefix) 길이 찾기
author: author1
tags: [EverydayProgramming]
category: [Algorithm]
---

[문제]  
문자열 배열(string array)이 주어지면, 제일 긴 공통된 접두사(prefix)의 길이를 찾으시오.  

[Question]  
Given an array of strings, find the longest common prefix of all strings.  

예제)
> Input: [“apple”, “apps”, “ape”]  
  Output: 2 // “ap”  

> Input: [“hawaii”, “happy”]  
  Output: 2 // “ha”  

> Input: [“dog”, “dogs”, “doge”]  
  Output: 3 // “dog”  

[풀이]  
제일 먼저 떠오르는 방법은, 이중 for문으로 한 char씩 검사하는 것이다.  
혹시 시간복잡도를 O(n)으로 줄일 수 있을까 해서 생각해보았지만 잘 모르겠다. 앞서 말한 풀이의 시간복잡도는 O(n^2)이다.  

전체 코드는 아래와 같이!  
~~~c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	vector<string> inputString;

	cout << "Input an array of strings: ";
	do { // 원하는 만큼 입력받기
		string temp;
		cin >> temp;
		inputString.push_back(temp);
	} while (getc(stdin) == ' ');

	int prefix = inputString[0].size(); // 첫 번째 string을 기준으로 비교
	for (int i = 1; i < inputString.size(); i++) {
		for (int j = 0; j < min(inputString[0].size(), inputString[i].size()); j++) {
			if (inputString[0][j] != inputString[i][j]) {
				prefix = min(prefix, j);
			}
		}
	}

	cout << "Output: " << prefix << endl;

	system("pause");
	return 0;
}
~~~

*문제 출처 - 2019매일프로그래밍*
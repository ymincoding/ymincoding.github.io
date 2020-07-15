---
layout: post
title: "[Everyday Programming]매일프로그래밍 #10"
description: >
  중복 없는 가장 긴 서브스트링 찾기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

❓__문제__❓  
String이 주어지면, 중복된 char가 없는 가장 긴 서브스트링 (substring)의 길이를 찾으시오. 

<br/>

❓__Question__❓  
Given a string, find the longest substring that does not have duplicate characters.

<br/>

예제)
> Input: “aabcbcbc”  
  Output: 3 // “abc”

> Input: “aaaaaaaa”  
  Output: 1 // “a”

> Input: “abbbcedd”  
  Output: 4 // “bced”
  

* * *

❗__풀이__❗  
제일 먼저 생각한 방법은 __이중for문__ 을 이용한 방법이었다.  
String을 하나씩 검사하면서 현재까지의 substring을 다시 하나씩 검사하는 방법이 제일 떠올리기 쉬운 방법이지만, 시간복잡도가 O(n^2)으로 높아지기 때문에 가장 효율적인 방법은 아니다.

시간복잡도를 __O(n)__ 으로 낮추기 위해 __Map__ 을 사용했다.
~~~c++
map<char, int> subString;
~~~
이러한 형태로, string을 하나씩 검사할 때 마다 각 char와 index를 넣어준다.

string을 검사하면서 map에 겹치는 문자가 없을 경우는 char와 index를 추가한다.
~~~c++
if (subString.find(inputString[i]) == subString.end()) { 
	// map에 겹치는 문자가 없을 경우
	subString[inputString[i]] = i; // string inputString
}
~~~

겹치는 문자가 있을 경우, 해당 문자의 index가 현재 검사중인 substring에 포함되는지 확인하고, 포함된다면 현재까지 가장 긴 substring의 길이를 계산하고 __substring의 시작점을 겹치는 문자 바로 다음 index로 지정__ 해서 새로운 substring을 고려할 수 있도록 한다. map에서 해당 문자의 index는 가장 최근 index로 변경한다.

~~~c++
#include <iostream>
#include <string>
#include <algorithm>
#include <map>
using namespace std;

int main() {
	cout << "Input: ";
	string inputString;
	cin >> inputString;

	int first = 0;
	int maximum = 1;
	map<char, int> subString;
	for (int i = 0; i < inputString.size(); i++) {
		if (subString.find(inputString[i]) == subString.end()) { 
			// map에 겹치는 문자가 없을 경우
			subString[inputString[i]] = i;
		}
		else {
			// 겹치는 문자가 있을 경우
			if (subString[inputString[i]] >= first) { // 현재 substring 안에 포함되는 문자인지
				maximum = max(i - first, maximum); // 가장 긴 substring 길이 갱신
				first = subString[inputString[i]] + 1;
			}

			subString[inputString[i]] = i; // 가장 최근 인덱스로 변경
		}
	}

	maximum = max((int)inputString.size() - first, maximum); // 가장 긴 substring 길이 갱신

	cout << "Output: " << maximum << endl;

	system("pause");
	return 0;
}
~~~

###### *문제 출처 - 2019매일프로그래밍*
---
layout: post
title: "[Everyday Programming]매일프로그래밍 #11"
description: >  
    암호화 가능한지 아닌지 확인하기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

[문제]  
길이가 같은 두 문자열(string) A 와 B가 주어지면, A 가 B 로 1:1 암호화 가능한지 찾으시오.  

[Question]  
Given two strings of equal length, check if two strings can be encrypted 1 to 1.  

예제)
> Input: “EGG”, “FOO”   
  Output: True // E->F, G->O  


[풀이]  
길이가 같은 두 문자열을 먼저 입력받는다.  
그리고 한 글자씩 비교를 하는데, 비교할 때 마다 비교 정보를 map에 저장한다.  
~~~c++
map<char, char> code; // <input1, input2>
~~~

찾는 문자가 map에 없으면 <input1, input2> 정보를 추가하고, 찾는 문자가 있지만 비교 정보가 다를 경우 암호화 불가능이라고 판단한다.  

~~~c++
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main() {
	string input1, input2;
	cout << "Input String 1: ";
	cin >> input1;
	cout << "Input String 2: ";
	cin >> input2;

	if (input1.size() != input2.size()) { // 길이가 다른 문자열이면 종료
		cout << "They have different lengths. Please try again." << endl;
		system("pause");
		return 0;
	}

	map<char, char> code;
	bool isItPossible = true;
	for (int i = 0; i < input1.size(); i++) {
		if (code.find(input1[i]) == code.end()) { // 찾는 문자가 없으면 추가
			code[input1[i]] = input2[i];
		}
		else {
			if (code.find(input1[i])->second != input2[i]) { // 찾는 문자는 있지만 암호화 문자가 다를 경우
				isItPossible = false;
				break;
			}
		}
	}

	if (isItPossible)
		cout << "Output: True" << endl;
	else
		cout << "Output: False" << endl;

	system("pause");
	return 0;
}
~~~


*문제 출처 - 2019매일프로그래밍*
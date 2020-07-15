---
layout: post
title: "[Everyday Programming]매일프로그래밍 #20"
description: >  
    2차원 배열 처음부터 모든 원소 방문 후에 다시 돌아오기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

❓__문제__❓  
정수 배열 arr이 있습니다. arr안의 각 원소의 값은 다음 원소의 인덱스입니다. 이렇게 서로 이어지는 원소들의 배열이 있을때, arr[0]부터 시작하여 모든 원소를 들린 다음 다시 arr[0]로 도착할 수 있는지 찾으시오.  
단, 시간복잡도는 O(n), 공간복잡도는 O(1).  

<br/>
예제)  
>Input: [1, 2, 4, 0, 3]  
 Output: True  
 // 1 -> 2 -> 4 -> 3 -> 0 -> 1  

>Input: [1, 4, 5, 0, 3, 2]  
 Output: False  
 // 1 -> 4 -> 3 -> 0 -> 1  
 // arr[2], arr[5]를 들리지 않았습니다.

>Input: [1, 2, 2, 0]  
 Output: False  
 // 1 -> 2 -> 2 -> 2 -> …  
 // arr[0]로 돌아오지 못합니다.

* * *

❗__풀이__❗  
vector를 이용해 배열 입력을 먼저 받는다. 그리고 같은 사이즈의 배열을 하나 만들어, 해당 인덱스의 방문 여부를 체크한다. 0이면 방문 전, 1이면 방문 후로 정한다.  
  
<br/>

`curIndex` 변수를 만들어 현재 가리키는 index를 나타내도록 하며, 0부터 시작한다.  
이동하려는 index가 0이면 방문하고 `curIndex`도 변경하고, 1이면 방문 했던 곳으로 돌아왔으므로 탐색을 마친다.  

<br/> 
  
탐색이 끝난 후, __방문 여부를 체크하는 배열에 0이 하나라도 존재하면 방문하지 않은 index가 있다는 뜻이므로 Output은 False, 모두 1이면 Output은 True!__  

<br/>  
  
전체 코드는 아래와 같이!  

<br/>
  
<span style="color: gray">*시간 복잡도는 맞춘 것 같은데, 공간복잡도에 대한 이해가 부족해서 맞았는지 모르겠다.. 더 공부해야지ㅠㅜ*</span>  
~~~c++
#include <iostream>
#include <vector>
using namespace std;

int main() {
	vector<int> indexArray;
	cout << "Input array: ";
	do {
		int temp;
		cin >> temp;
		indexArray.push_back(temp);
	} while (getc(stdin) == ' ');

	int* check = new int[indexArray.size()];
	for (int i = 0; i < indexArray.size(); i++) {
		check[i] = 0;
	}

	int curIndex = 0;
	check[curIndex] = 1;
	while (true) {
		if (check[indexArray[curIndex]] == 0) { // 이동하려는 위치가 0으로 표기되있으면 아직 방문 안한것!
			curIndex = indexArray[curIndex];
			check[curIndex] = 1;
		}
		else { // 이미 방문했다고 표기된 경우
			break;
		}
	}

	int j;
	for (j = 0; j < indexArray.size(); j++) {
		if (check[j] == 0) {
			cout << "Output: False" << endl;
			break;
		}
	}
	if (j == indexArray.size()) { // 모두 방문 한 경우
		cout << "Output: True" << endl;
	}

	system("pause");
	return 0;
}
~~~

*문제 출처 - 2019매일프로그래밍*
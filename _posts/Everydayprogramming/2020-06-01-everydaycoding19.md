---
layout: post
title: "[Everyday Programming]매일프로그래밍 #19"
description: >  
    2차원 배열 소용돌이 모양으로 출력하기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

[문제]  
2차 정수 배열(2D int array)가 주어지면, 소용돌이 모양으로 원소들을 프린트하시오. 예제를 보시오.  

[Question]  
Given a 2D integer array, print all elements in a circular spiral shape starting from [0][0]. See example.  

예제)  
> Input:  
  [[1, 2, 3],  
  [8, 9, 4],  
  [7, 6, 5]]  
  Output:  
  1, 2, 3, 4, 5, 6, 7, 8, 9 

* * *

[풀이]  
2차원 배열의 행, 열의 크기를 알고 행의 처음과 끝, 열의 처음과 끝을 변수에 저장한다.  
그리고 `rowCur`, `colCur` 변수에 현재 위치를 저장하고, 한 칸씩 이동하며 배열을 출력한다.  
  
방향이 오른쪽이면 오른쪽 벽에 닿을 때 까지 출력하고, `colCur`를 오른쪽으로 이동한다. 만약 오른쪽 벽에 닿으면 아래쪽으로 방향을 변경한다. 이 때, 첫 행은 모두 출력을 완료한 상태이므로 더 이상 첫 행은 출력하지 않는다는 뜻에서 `rowFirst`를 한 줄 아래로 이동한다. 이제부터는 제일 위 벽이 한 줄 아래로 내려왔다.  
  
방향이 아래쪽으로 변경되었으면 벽에 닿을 때 까지 출력하고, `rowCur`를 아래쪽으로 이동한다. 만약 아래쪽 벽에 닿으면 왼쪽으로 방향을 변경한다(bool right 변수를 false로 설정). 이 때, 마지막 열은 출력을 모두 완료한 상태이므로 더 이상 마지막 열은 출력하지 않는다는 뜻에서 `colLast`를 하나 줄인다.  
  
이와 같이 왼쪽 방향, 위쪽 방향까지 완료한다!  
마지막으로, `rowCur`와 `colCur`가 이동할 방향이 없으면 반복문을 종료한다.  
  
전체 코드는 아래와 같이!  
~~~c++
#include <iostream>
using namespace std;

int main() {
	const int input[3][3] = { {1, 2, 3}, {4, 5, 6}, {7, 8, 9} };
	//const int input[4][3] = { {1, 2, 3}, {4, 5, 6}, {7, 8, 9}, {10, 11, 12} };

	int rowFirst = 0;
	int rowLast = 2;
	int colFirst = 0;
	int colLast = 2;

	int rowCur = rowFirst;
	int colCur = colFirst;
	bool right = true; // 현재 진행 방향 오른쪽
	bool down = true; // 현재 진행 방향 아래쪽
	
	while (true) {
		cout << input[rowCur][colCur] << " ";

		if (right && colCur < colLast) { // 오른쪽으로 진행
			colCur++;

			if (colCur == colLast) {
				down = true;
				rowFirst++;
			}
		}
		else if (down && rowCur < rowLast) { // 아래로 진행
			rowCur++;

			if (rowCur == rowLast) {
				right = false;
				colLast--;
			}
		}
		else if (!right && colCur > colFirst) { // 왼쪽으로 진행
			colCur--;

			if (colCur == colFirst) {
				down = false;
				rowLast--;
			}
		}
		else if (!down && rowCur > rowFirst) { // 위쪽으로 진행
			rowCur--;

			if (rowCur == rowFirst) {
				right = true;
				colFirst++;
			}
		}
		else { // 종료
			break;
		}
	}

	system("pause");
	return 0;
}
~~~

*문제 출처 - 2019매일프로그래밍*
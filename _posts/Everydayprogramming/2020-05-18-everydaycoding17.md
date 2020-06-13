---
layout: post
title: "[Everyday Programming]매일프로그래밍 #17"
description: >
    가장 가까운 길의 거리 찾기
author: Yunmin Cho
tags: [EverydayProgramming]
category: [Algorithm]
---

[문제]  
0과 1로 만들어진 2D 정수 배열이 있습니다. 0은 장애물이고 1은 도로일때, 두 좌표가 주어지면, 첫번째 좌표에서 두번째 좌표까지 가장 가까운 거리를 구하시오. 두 좌표는 모두 도로에서 시작되고 좌, 우, 아래, 위로 움직이며 대각선으로는 움직일 수 없습니다. 만약 갈 수 없다면 -1을 리턴하시오.  

[Question]  
Given a 2D array with 0s and 1s, 0 represents an obstacle and 1 represents a road. Find the closest distance between two given points. You must only move up down right left. You cannot move through an obstacle.  

예제)  
> Input:  
  1, 0, 0, 1, 1, 0,  
  1, 0, 0, 1, 0, 0,  
  1, 1, 1, 1, 0, 0,  
  1, 0, 0, 0, 0, 1,  
  1, 1, 1, 1, 1, 1  
  Start: (0, 0)  
  Finish: (0, 4)  
  Output: 8  

[풀이]  
지금까지 문제중에 제일 어렵게 푼 것 같다.  
가장 먼저 생각나는 방법은 __재귀함수__ 이다. 하지만 재귀함수를 만드려면 main함수에서 가지고있는 변수들을 전부 파라미터로 넘겨주거나 전역변수로 설정해야한다. 그래서 효율성을 비교하진 못했지만, __while문으로 재귀함수를 이용하지 않고 풀어보았다.__  

<span style="color: #FCBD2B">** *현명하지 않은 선택이었던 것 같다.ㅎㅎ 다양한 방법을 시도해보는데에 의의를 두었다. 풀지 못하신 분은 다른 재귀함수 코드를 참고하시길 추천ㅠㅜ*</span>  

맵 사이즈를 입력 받고, 시작점과 끝점을 입력받는다.  
입력받은 크기의 배열로 맵을 만드는데, 이때 temp 맵을 하나 더 만들고 전부 0으로 초기화한다. 지나간 길을 표시하기 위한 맵이다.  

__<span style="color: var(--highlight-color)">지나간 길의 좌표는 Stack에 저장한다.</span>__ 재귀함수가 마치 stack의 역할과 같아서, 지나간 순서대로 stack에 저장되고, 길이 없어서 다시 돌아가야한다면 stack에 마지막에 저장된 길로 돌아가는 것이다.  
시작점을 pastRoad 스택에 저장하고 시작하고, arrTemp에 지나간 길이라는 표시로 해당 좌표를 1로 변경한다.
~~~c++
stack<int*> pastRoad;
int start[2] = { startX, startY };
pastRoad.push(start);
arrTemp[startY][startX] = 1;
~~~  

이제 재귀함수 대신 while문을 도는데, __종료 조건__ 은 다음과 같다.  
1. 길이 없다 -> stack size가 0이다.  
2. 길을 찾았다 -> 현재 좌표가 끝점의 좌표와 같다.  

이동은 대각선이 아닌 위아래와 양옆만 가능하다고 했다. 그래서 4방향 중 0이 아닌 1인 방향만 찾고, 최종 목적지까지의 거리를 계산해서 가장 가까운 방향으로 이동한다. 이동한 좌표는 stack에 넣어준다.  
![Ex1](/assets/img/programming/everydaycoding17_1.JPG)
이 경우에는 3번 방향으로만 이동이 가능하다.  

최종 목적지까지의 거리가 가장 가까운 점으로 이동하기 위해, 두 점 사이의 거리를 측정해야 한다. 두 점의 좌표를 파라미터로 넣어준다.  
~~~c++
float fnDistance(int sx, int sy, int fx, int fy) {
	return sqrt(pow(fy-sy, 2) + pow(fx-sx, 2));
}
~~~

네 방향을 다 확인한 후에, __최종 목적지와 가장 가까운 방향을 stack에 넣어준다.__ 해당 좌표는 지나간 길이기 때문에 __arrTemp의 해당 좌표를 1로 변경한다.__ __<span style="color: var(--highlight-color)">만약 더 이상 이동할 길이 없는 경우(전부 0이거나, 1이지만 이미 지나온 길로 체크되어 있거나) stack의 top을 제거한다.</span>__
~~~c++
stack.pop()
~~~

이렇게 while문을 반복하다 종료조건을 만족하면 stack의 size를 출력한다. 이때, 예를들어 stack size가 3이라고 하면, 이동한 거리는 2이기 때문에 size-1을 출력한다.  

전체 코드는 아래와 같이!
~~~c++
#include <iostream>
#include <ctime>
#include <stack>
using namespace std;

float fnDistance(int sx, int sy, int fx, int fy);

int main() {
	// 가로 세로 크기 입력받아서 랜덤 맵 생성하기
	int rowN, colN;
	cout << "Input row number: ";
	cin >> rowN;
	cout << "Input col number: ";
	cin >> colN;

	srand(time(NULL));
	int** arrMap = new int*[rowN]; // 맵 생성
	int** arrTemp = new int*[rowN]; // 지나온 길 확인용
	for (int i = 0; i < rowN; i++) {
		arrMap[i] = new int[colN];
		arrTemp[i] = new int[colN];
		for (int j = 0; j < colN; j++) {
			arrMap[i][j] = rand() % 2;
			arrTemp[i][j] = 0;
		}
	}

	for (int i = 0; i < rowN; i++) {
		for (int j = 0; j < colN; j++) {
			cout << arrMap[i][j] << " ";
		}
		cout << endl;
	}

	int startX, startY;
	int finishX, finishY;
	while (true) {
		cout << "Start row col number: ";
		cin >> startY >> startX;
		if (arrMap[startY][startX] != 1) {
			cout << "You can choose only 1 position." << endl;
		}
		else
			break;
	}
	while (true) {
		cout << "Finish row col number: ";
		cin >> finishY >> finishX;
		if (arrMap[finishY][finishX] != 1) {
			cout << "You can choose only 1 position.: " << endl;
		}
		else
			break;
	}
 	
	stack<int*> pastRoad;
	int start[2] = { startX, startY };
	pastRoad.push(start);
	arrTemp[startY][startX] = 1;

	while (pastRoad.size() > 0) {
		int* current = pastRoad.top(); // 현재 좌표

		if (current[0] == finishX && current[1] == finishY) // 길을 찾은 경우
			break;

		float distance[4] = { -1, -1, -1, -1 };
		if (current[1] != 0 && arrMap[current[1]-1][current[0]] == 1) { // 위 방향 확인
			distance[0] = fnDistance(current[0], current[1] - 1, finishX, finishY);

			if (arrTemp[current[1] - 1][current[0]] == 1) // 바로 전에 지나온 길이면
				distance[0] = -1;
		}

		if (current[0] != colN - 1 && arrMap[current[1]][current[0] + 1] == 1) { // 오른쪽 방향 확인
			distance[1] = fnDistance(current[0] + 1, current[1], finishX, finishY);

			if (arrTemp[current[1]][current[0] + 1] == 1) // 바로 전에 지나온 길이면
				distance[1] = -1;
		}

		if (current[1] != rowN - 1 && arrMap[current[1] + 1][current[0]] == 1) { // 왼쪽 방향 확인
			distance[2] = fnDistance(current[0], current[1] + 1, finishX, finishY);

			if (arrTemp[current[1] + 1][current[0]] == 1) // 바로 전에 지나온 길이면
				distance[2] = -1;
		}

		if (current[0] != 0 && arrMap[current[1]][current[0] - 1] == 1) { // 아래쪽 방향 확인
			distance[3] = fnDistance(current[0] - 1, current[1], finishX, finishY);

			if (arrTemp[current[1]][current[0] - 1] == 1) // 바로 전에 지나온 길이면
				distance[3] = -1;
		}

		int minIndex = -1;
		for (int i = 0; i < 4; i++) {
			if (distance[i] != -1) {
				if (minIndex == -1) {
					minIndex = i;
				}
				else {
					if (distance[minIndex] > distance[i]) {
						minIndex = i;
					}
				}
			}
		}

		if (minIndex == -1) { // 길이 없음
			pastRoad.pop();
			continue;
		}

		int newRoad[2];
		switch (minIndex) {
		case 0: 
			newRoad[0] = current[0]; newRoad[1] = current[1] - 1;
			break;
		case 1: 
			newRoad[0] = current[0] + 1; newRoad[1] = current[1];
			break;
		case 2: 
			newRoad[0] = current[0]; newRoad[1] = current[1] + 1;
			break;
		case 3: 
			newRoad[0] = current[0] - 1; newRoad[1] = current[1];
			break;
		default: 
			break;
		}
		arrTemp[newRoad[1]][newRoad[0]] = 1; // 지나간 길 표시
		pastRoad.push(newRoad);
	}

	if (pastRoad.size() == 0)
		cout << endl << "Output: No road connected" << endl; // 길 없음
	else
		cout << endl << "Output: " << pastRoad.size() - 1 << endl;

	system("pause");
	return 0;
}

float fnDistance(int sx, int sy, int fx, int fy) {
	return sqrt(pow(fy-sy, 2) + pow(fx-sx, 2));
}
~~~


*문제 출처 - 2019매일프로그래밍*
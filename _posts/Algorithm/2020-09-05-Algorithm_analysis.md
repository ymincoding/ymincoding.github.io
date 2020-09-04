---
layout: post
title: "[Algorithm]시간복잡도와 공간복잡도(Time and space complexity)"
description: >
    시간복잡도(Time complexity) - 입력 크기에 따라 단위연산이 몇 번 수행되는지 결정하는 절차   
    공간복잡도(Space complexity) - 입력 크기에 따라 작업공간(메모리)이 얼마나 필요한지 결정하는 절차
author: Yunmin Cho
tags: [Algorithm]
category: [Algorithm]
---  

📌 __공간 복잡도(Space Complexity)__  
- 알고리즘의 입력 크기에 따른 필요한 작업공간(메모리)  

📌 __시간 복잡도(Time Complexity)__  
- 알고리즘을 수행하는 데 걸리는 시간  
- 입력 크기에 따라 수행되는 단위 연산 횟수  

<br/>  

<span style="color: #FF9900">공간 복잡도도 물론 중요하지만, 시간 복잡도를 줄이는 것에 더 집중해야 함!</span>   
  
---  

📌분석 방법의 종류  
1. Every-case analysis(모든 경우 분석)  
- 입력 자료 크기에 영향을 받고, 입력 값과는 무관함  

2. <span style="color: #FF0000">Worst-case analysis(최악의 경우 분석)</span>  
- 입력 자료의 크기와 입력 값 모두 영향을 받음  
- 알고리즘 수행 시간이 최악인 경우(가장 많이 수행되는 경우)를 분석  

3. Average-case analysis(평균의 경우 분석)  
- 모든 입력에 대해서 알고리즘이 수행되는 시간들의 평균  

4. Best-case analysis(최선의 경우 분석)  
- 입력 자료의 크기와 입력 값 모두 영향을 받음  
- 알고리즘 수행 시간이 최선인 경우(가장 적게 수행되는 경우)를 분석  

<br/>  

✔ __순차검색 시간 복잡도__  
~~~c++
location = 1;
while(location <= n && S[location] != x){
    location++;
}
if(location > n){
    location = 0;
}
~~~  
- 단위 연산: 배열의 값과 키 x의 비교 연산  
- 입력 크기: 배열의 크기 n  
- 최악의 경우 분석: x가 배열의 마지막 아이템이거나, x가 배열에 없는 경우 단위 연산 n번 수행됨  
__W(n) = n__  

<br/>  

---  
📌 __Big-O(빅오) 표기법__  
- 점근적 상한(Asymptotic upper bound)를 제공, 즉 최악의 경우를 표기하는 방법  
- 어떤 알고리즘의 시간 복잡도가 O(f(n)) 이라면, 입력 크기 n에 대하여 이 알고리즘은 아무리 늦어도 f(n) * c(상수)는 된다, 즉 최악의 경우가 f(n)이라는 뜻이다.  

<br/>  

✔ 대표적인 복잡도 함수  
- 이진탐색: O(log n)  
- 순차검색: O(n) <span style="color: gray">*1차(linear)*</span>  
- 퀵소트: O(n log n)  
- 삽입정렬, 행렬 덧샘 등: O(n^2) <span style="color: gray">*2차(quadratic)*</span>  
- 행렬의 곱: O(n^3) <span style="color: gray">*3차(cubic)*</span>  
- 두 가지 경우의 수 중 선택하는 연산: O(2^n) <span style="color: gray">*지수(exponential)*</span>  

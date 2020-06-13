---
layout: post
title: "[Graphics]그래픽스 Transformation 기초"
description: >  
    컴퓨터 그래픽스 이론 공부 - Transformation
author: Yunmin Cho
tags: [Graphics]
category: [Graphics]
---

📌__Transformation Groups__  
- 아래 3가지 조건을 만족하는 원소들로 이루어진 집합  
    1. 연산에 대하여 닫혀있는 집합  
    _A &isin; G_ and _B &isin; G_ __->__ _A*B &isin; G_  
    2. 다음을 만족하는 I가 존재하는 집합  
    _A*I = I*A = A_  
    3. 역행렬을 가지는 집합  
    _A^-1 *A = A* A^-1 = I_  

![ex1](/assets/img/programming/transformation_1.JPG){:.width-50}
3가지 조건을 만족하면 어떤 방향으로, 어떤 연산을 먼저 하더라도 같은 결과가 나올 것이고, 그 반대의 연산도 가능해진다.  

* * *

📌__Scale__  
![](/assets/img/programming/transformation_2.JPG){:.width-50}
- 위치, 모양 변하지 않고 크기만 변하는 것  
- 형태가 변하지 않는다면 비율을 나타내는 변수 한개면 됨  
- 변수가 s1, s2로 2개라면, 방향에 따라 다르게 scaling하는 것  
- 원점 기준 scaling  

* * * 

📌__Rotation__  
![](/assets/img/programming/transformation_3.JPG){:.width-50} 
- 2차원 Rotation: 변수 1개  
- 3차원 Rotation: 변수 3개 필요(x방향, y방향, z방향)  

* * * 

📌__Euclidean(Rigid)__  
![](/assets/img/programming/transformation_4.JPG){:.width-50} 
- 형태가 변하지 않는 transformation  
- Rotation + Translation
- 다음과 같이 표현 가능: _`p' = Rp + t`_ (R: Rotation, t: Translation)  

* * *  

📌__Similarity(scaled Euclidean)__  
![](/assets/img/programming/transformation_5.JPG){:.width-50}  
- Scale + Rotation + Translation  
- 2차원 Similarity: 변수 4개 필요(s, R, tx, ty)  
- 3차원 Similarity: 변수 7개 필요(s, Rx, Ry, Rz, tx, ty, tz)  

* * *  

📌__Affine__  
![](/assets/img/programming/transformation_5.JPG){:.width-50}  
- 평행을 유지하며 기울일 수 있는 변환  
- 변수 총 6개: s, R, x축 기울임 정도, y축 기울임 정도, tx, ty  

* * *

📌__Projective__  
![](/assets/img/programming/transformation_5.JPG){:.width-50}    
- 3차원에서 2차원으로 투영할 때 생기는 변환  
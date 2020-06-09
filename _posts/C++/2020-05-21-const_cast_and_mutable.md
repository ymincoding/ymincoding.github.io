---
layout: post
title: "[C++문법] const_cast와 mutable"
description: >
    [C++문법]상수성을 제거하는 const_cast와, 상수 멤버 함수 내에서도 수정할 수 있는 mutable
author: author1
tags: [C++]
category: [C++]
---
<span style="color: var(--highlight-color)"> const는 변수나 함수에 상수성을 적용할 때 사용된다. </span> 변경 불가능한 상태로 만들어 프로그래머나 사용자 모두에게 알리는 것이다. 하지만 때에 따라, 상수성이 제거되어양 할 필요도 있다.  

### 1. const_cast
- 형태: const_cast<바꿀타입>(대상)  
- const로 정의된 변수의 상수성을 제거해주는데 사용  
- 포인터나 참조로만 캐스팅이 가능!  
- 상수성을 추가도 가능하지만, 굳이..?  (const_cast<const int*> 이런식으로)  
- 상수성 유무 변경 가능하지만, 기본 type은 변경 불가! (int를 상수성 제거한 char로, char를 상수성 제거한 int로 불가)  

~~~c++
#include <iostream>

int main(){
    const int a = 6; // 상수 데이터
    const int * pa = &a; // 비상수 포인터로 상수 데이터를 가리킴
    int * p = pa; // ERROR!!

    int * pp = const_cast<int*>(pa); // 상수성을 제거해주고 가리키도록 하면 가능
}
~~~

### 2. mutable
클래스 내에서 const로 멤버 함수를 설정했을 경우, 함수 내부에서 멤버 변수의 값을 변경하는 것이 불가능하다.  
하지만 멤버 변수를 <span style="color: var(--highlight-color)"> mutable </span> 로 선언했을 경우, 이 멤버 변수들은 어떤 순간에도 수정이 가능해진다.  

~~~c++
class A{
private: 
    int memA;
    mutable int memB;
public:
    void setMemA(int temp) const {
        memA = temp; // ERROR!!! 상수 함수에서 비상수 멤버 변수 변경 불가!
    }

    void setMemB(int temp) const{
        memB = temp; // 가능! memB는 mutable이기 때문에 상수함수에서도 변경 가능!
    }
};
~~~
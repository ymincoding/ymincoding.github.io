---
layout: post
title: "[Effective C++] #define을 쓰려거든 const, enum, inline을 떠올리자"
description: >
    C++의 선행 처리자, #define을 대신할 수 있는 것들
author: Yunmin Cho
tags: [C++]
category: [C++]
---
##### #define - 선행처리자
1) 단순한 문자열의 치환  
2) 다른 파일의 내용을 첨가  
3) 컴파일러에게 컴파일 조건 부여  
4) 컴파일러에게 정보 제공  

*주로 상수를 정해놓고 쓸 때 #define을 이용하지만 상습적으로 이용하는 것은 효과적이지 못하다.  
#define 대신 사용할 수 있는 방법들이 있다.  

### 1. [const]를 이용하자  
<span style="color: var(--highlight-color)"> #define ASPECT_RATIO 1.653 </span>  
- 컴파일러에게 넘어가기 전에 선행 처리자가 상수 이름 대신 숫자로 싹 바꾸어버림  
- ASPECT_RATIO는 컴파일러가 쓰는 기호 테이블에 들어가지 않는다. -> 에러가 나도 이름이 안뜨고 숫자 1.653이 뜨니, 어디서 에러가 났는지 알기 어려움  
- ASPECT_RATIO가 등장한 자리마다 상수 숫자가 들어가므로 등장한 만큼 사본 생김  
- 일단 정의되면 컴파일이 끝날 때까지 유효

<span style="color: var(--highlight-color)"> const double AspectRatio = 1.653 </span>  
- 컴파일러의 기호 테이블에 들어갈 때 변수 이름으로 들어감  
- 사본 딱 한개  


### 2. 클래스 멤버로 상수를 사용한다면 [static]  
클래스 멤버로 이용하고 싶은데, 사본을 한개만 만들어 상수로써 이용하고 싶다면 __static__ 을 이용하자.
__정적 멤버__ 란, 클래스에는 속하지만 객체 별로 할당되지 않고 클래스의 모든 객체가 공유하는 멤버를 의미한다.  
~~~c++
class GamePlayer{
    private: 
        static const int Numturns = 5; // 상수 선언
        int scores[NumTurns];
};
~~~  

### 3. 열거형 [enum] 사용하기  
열거된 유형이 상수로 정의되는 자료형이다.  
~~~c++
enum Fruit{
    FRUIT_APPLE, // 1 할당됨
    FRUIT_ORANGE, // 2 할당됨
    FRUIT_BANANA // 3 할당됨
};

Fruit mine = FRUIT_APPLE;
Fruit yours = FRUIT_BANANA;
~~~

- enum 선언만으로 주소가 할당되지는 않는다! #define과 마찬가지로 주소를 취할 수 없음  
- cout 으로 출력하면 할당된 정수값이 출력됨  
- 값을 임의로 수정 불가 (static_cast로 강제 변환은 가능)  

### 4. 매크로 함수 대신 [inline]함수  
일반적인 함수를 사용하면 함수를 호출할 때, 현재 명령어의 주소를 저장하고 함수를 호출하여 실행한 후 다시 저장된 명령어의 주소로 돌아와서 원래의 코드를 진행한다.   
__inline 함수__ 는, 함수를 호출하여 이동하는 것이 아니라 함수 내용 코드를 그대로 복사해서 함수 자리에 그대로 붙여넣어 실행한다. 현재 명령어의 주소를 저장할 필요도, 함수를 새로운 주소를 할당해서 실행할 필요도 없다.  

아래와 같이 inline으로 설정하면,   
~~~c++
inline int add(int a, int b){
    return a+b;
}

int main(){
    cout << add(2, 3) << endl;
}
~~~

컴파일러는 아래와 같이 읽는다.  
~~~c++
int main(){
    cout << 2+3 << endl;
}
~~~  

*출처: [Effective C++] 책 + 나의 추가정리*
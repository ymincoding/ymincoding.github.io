---
layout: post
title: "[C++]Initialize List(초기화 리스트)"
description: >
    C++ 문법 - Initialize List(초기화 리스트) 개념 및 필요성
author: Yunmin Cho
tags: [C++]
category: [C++]
---

📌__초기화 리스트(Initialize List)란__  
C++에서 Class의 멤버변수들을 초기화 할 때, Class 생성자 뒤에 :을 이용해 초기화 하는 것이다.  
~~~c++
class Rectangle{
private: 
    int rowLength;
    int colLength;
public:
    Rectangle(int rL, int cL):rowLength(rL), colLength(cL)
    {}
    ~Rectangle()
};
~~~

초기화리스트를 사용하지 않은 경우, 생성자 안에서 rowLength와 colLength를 아래와 같이 초기화한다.  
~~~c++
class Rectangle{
private: 
    int rowLength;
    int colLength;
public:
    Rectangle(int rL, int cL)
    {
        rowLength = rL;
        colLength = cL;
    }
    ~Rectangle()
};
~~~

하지만 엄밀히 말하면, 이것은 <span style="color: var(--highlight-color)">초기화가 아니라 대입</span>이다. 생성자의 내부에 들어가기 전 이미 기본생성자를 통해 초기화 되었고, 그 후 멤버변수들에 rL과 cL을 __대입__ 하는 것이다.  

> 초기화 리스트를 통해 멤버를 초기화하는 습관을 들일 것!
           - _<Effective C++> 책 중_ 

* * *

📌__초기화 리스트가 반드시 필요한 순간__  
__1. 상수 멤버 변수 초기화__  
`const`가 붙은 상수 멤버는 무조건 변경이 불가능하기 때문에, 초기화 리스트를 사용하지 않고 생성자 내부에서 대입하는 방식은 불가능하다. 꼭 초기화리스트 이용!  
~~~c++
class Circle{
private: 
    int r;
    const float pi;
public:
    Circle(int inputR, float inputPI): pi(inputPI) // 상수는 대입 안되므로 반드시 초기화 리스트
    {
        r = inputR; // r은 상수가 아니기 때문에 상관없음
    }
    ~Circle()
};
~~~

__2. Base Class 멤버 변수 초기화 할 때__  
상속을 하고 있다면, 자식 클래스의 멤버가 초기화되기 전에 부모 클래스가 초기화되어야 한다.
~~~c++
class Parent{
private:
    int A;
public:
    Parent(int a): A(a) {}
    ~Parent()
};

class Child : public Parent{
private: 
    int B;
public:
    Child(int a): Parent(a)
    {
        B = b; 
    }
    ~Child()
};
~~~

* * *

반드시 필요한 순간이 더 있을텐데, 공부하면서 추가해야겠다..!
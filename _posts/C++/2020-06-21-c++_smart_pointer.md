---
layout: post
title: "[C++]Smart Pointer(스마트 포인터)"
description: >
    C++ 문법 - Smart Pointer(스마트 포인터) 개념 및 사용 방법
author: Yunmin Cho
tags: [C++]
category: [C++]
---

일반적인 포인터는 heap memory에 저장된 자원에 접근할 때 쓰인다.  
~~~c++
Rectangle* p = new Rectangle()
~~~  
이렇게 선언한 포인터는 반드시 자원을 해제해주어야 한다. 그렇지 않으면 heap memory에는 `new Rectangle()`로 인해 메모리가 할당은 되었으나 해제되지 않아 메모리 누수가 발생한다.  
<br/>

📌__Smart Pointer(스마트 포인터)란?__  
C++에서 제공하는 스마트 포인터는, 자동으로 메모리를 관리하여 포인터가 사용되지 않을 때에는 자동으로 자원을 해제해주는 포인터이다. 일반 포인터는 명시적으로 `delete`를 호출하여 해제해주어야 하는 반면, 스마트 포인터는 지역을 빠져나가면 자동으로 `deallocation`을 실행해준다.  

<br/>

~~~c++
Object* ptr = new Object(); // new를 통해 메모리 할당됨
ptr->callfunction();
// delete 없음
~~~
일반 포인터를 사용할 경우, `new`연산자를 통해 Object 객체를 새로운 메모리에 할당한다. 함수 안에서 위의 코드를 사용했거나, 프로그램이 끝났을 경우 지역을 벗어나게 되면 지역 안에서 할당된 변수인 포인터는 지역변수이기 때문에 사라진다. 하지만 `new`로 할당된 Object는 delete를 통해 해제해주지 않았으므로 메모리에 남아있게 된다.  
__스마트 포인터를 사용할 경우, delete를 명시적으로 사용하지 않아도 소멸자가 실행되면서 자원 해제를 자동으로 해준다!__  

<br/>
* * *
<br/>
📌 __Types of Smart Pointer(스마트 포인터의 종류)__  

1. unique_ptr  
    - `unique_ptr`로 한 객체를 가리키면, 한 객체는 오직 한 개의 포인터로만 접근 가능하다. 다른 포인터와 공유할 수 없지만, 이전은 가능하다. 그럴 경우 원래의 포인터는 삭제된다.  

2. shared_ptr  
    - `unique_ptr`과 달리, 여러 포인터가 동시에 한 객체를 가리키는 것이 가능하다. 이 때 `shared_ptr`은 공유되고 있는 포인터의 개수를 카운트한다(Reference Counter). `use_count()` 함수를 통해 확인할 수 있다. 또한 자신이 참조하고 있는 객체 하나가 소멸되더라도, 동일한 메모리 주소를 가리키는 다른 shared_ptr가 있으면 객체는 소멸되지 않는다.(dangling pointer 방지)  

3. weak_ptr  
    - 공유되고 있는 포인터의 개수(Reference Counter)를 카운트 하지 않는다는 점을 제외하면 `shared_ptr`과 거의 비슷하다. shared_ptr의 객체만 참조할 수 있을 뿐, shared_ptr의 reference counter를 올리지 않는다.  
    - 같은 weak_ptr 또는 shared_ptr로부터 복사 생성, 대입 연산이 가능하고, shared_ptr로만 변환할 수 있다.  
    - 특정 객체를 참조하면서 수명에는 영향을 주고 싶지 않은 경우, 동시에 dangling pointer를 막고싶은 경우  

4. auto_ptr
    - 참조하고 있는 대상에 대해 소멸자가 자동으로 delete 해주는 포인터로, dangling pointer를 막는다.  
    - `auto_ptr`을 복사하면 원본 객체는 null이 된다.  
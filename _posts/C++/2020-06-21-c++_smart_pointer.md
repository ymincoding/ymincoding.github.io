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

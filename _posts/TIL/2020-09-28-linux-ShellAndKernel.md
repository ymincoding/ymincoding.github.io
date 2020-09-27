---
layout: post
title: "[Linux]쉘과 커널(SHELL vs KERNEL)"
print: True
modal: True
image: #"IORedirection2.JPG" #path: assests/til/
description: 리눅스 공부 - 쉘과 커널
category: [TIL]
---

📍 __쉘과 커널(SHELL vs KERNEL)__  
![Shell and kernel](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F27552535590AB2BB0F)  
- Kernel이 하드웨어를 감싸고, Shell이 Kernel을 감싸는 형태이다. 즉, <span style="color: #FF8000">Shell을 통해서 입력된 명령어들이 Kernel로 전달되고, Kernel에서 하드웨어가 이해할 수 있는 형태로 해석해서 명령어를 전달한다.</span>  
- Shell을 통해서 입력된 명령어들이 Kernel로 전달되는데, Shell이 Kernel과 분리됨으로써 더욱 다양한 형태의 Shell이 존재한다. 사용자의 편의성에 맞는 Shell을 사용할 수 있다.  
  
<br/>

📍 __bash vs zsh__  
- Shell의 여러가지 종류 중 2가지, bash와 zsh.  
- 사용자가 원하는 Shell을 선택해서 사용할 수 있다.  
- bash가 기본으로 설치되는 경우가 많고, zsh가 몇 가지 편리한 추가기능을 제공하기도 한다.  
- 현재 자신의 Shell을 확인하고 싶을 때 명령어: `echo $0`  

<br/>  
<span style="color: gray"> _출처: https://opentutorials.org/course/2598/14199_ </span>
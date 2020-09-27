---
layout: post
title: "[Linux]IO Redirection"
print: True
modal: True
image: "IORedirection2.JPG" #path: assests/til/
description: 리눅스 공부 - IO Redirection
category: [TIL]
---

📍 __IO Redirection__  
- Input Output Redirection: 입력과 출력의 방향을 바꾼다.  

<br/>

__기존 ls 명령어__  
- `ls -al` 명령어를 입력하면 현재 보고있는 모니터에, 현재 디렉토리 안에 들어있는 모든 폴더와 파일들(숨김파일 포함)을 출력해준다.  
![기존 ls명령어]({{ site.baseurl }}/assets/til/IORedirection1.jpg){:.width-100}  

__IO Redirection 적용__  
- 출력의 방향을 현재 모니터가 아닌 특정 파일로 변경하고 싶을 경우  
- 현재 모니터에는 아무것도 출력되지 않고, 명령어 실행 결과 출력을 파일에 저장한다.  
![Redirection]({{ site.baseurl }}/assets/til/IORedirection2.JPG){:.width-100}  

<br/>

📍 __>의 의미__  
- `ls -al > result.txt` 에서 > 명령어는, `1>`의 생략이다.  
- `1>`는 Standard Output의 결과를 출력한다.  
- 즉, Standard Error의 경우 적용이 안된다.  
- Standard Error에 Redirection을 적용하고 싶으면 `2>`를 사용한다.  
![Standard Error Redirection]({{ site.baseurl }}/assets/til/IORedirection3.JPG){:.width-100}  
1. `rm result.txt`를 두 번 입력하면, 이미 없는 파일인 result.txt 를 지우려고 하는 명령이므로 에러가 발생하고 Error 메시지를 출력한다.  
2. `rm result.txt > rm_result.txt` 명령어로 Error 메시지를 rm_result.txt 파일에 저장하려고 하지만, 여전히 화면에 Error 메시지가 출력된다. `>` 명령어는 `1>`의 생력으로, Standard Output에만 적용되기 때문이다.  
3. Standard Error에 적용하기 위해, `rm result.txt 2> error.log` 명령어를 사용한다.  
4. 화면에 Error 메시지는 출력되지 않고, `cat error.log`를 통해 error.log 파일을 살펴보면 Error 메시지가 저장된 것을 확인할 수 있다.  

<br/>  
<span style="color: gray"> _출처: https://opentutorials.org/course/2598/14199_ </span>
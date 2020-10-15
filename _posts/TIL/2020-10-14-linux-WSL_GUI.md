---
layout: post
title: "[Linux]WSL에서 GUI프로그램 실행하기"
print: True
modal: True
image: #"IORedirection2.JPG" #path: assests/til/
description: 리눅스 공부 - WSL에서 GUI프로그램 실행하기
category: [TIL]
---

<span style="color: gray"> _출처: https://wnsgml972.github.io/setting/2019/05/07/wsl/  
모든 자료 이 블로그에서! 아래는 내가 보고 설치한 것들만 한 번 더 정리_ </span>  

<br/>

__WSL: Microsoft에서 제공하는 리눅스용 윈도우 하위시스템(Windows Subsystem for Linux)__  

<br/>

WSL만으로는 GUI프로그램을 실행할 수 없음  
➡ <span style="color: red">Windows용 X org서버를 설치하고 실행해야 함!</span>  

<br/>

📌 __Windows용 X org 서버 설치하고 실행__  
- `vcxsrv` 서버 다운로드  
- https://sourceforge.net/projects/vcxsrv/  

<br/>

📌 __WSL 환경 설정 및 테스트__  
1. `/etc/machine-id/` 파일 생성  
~~~bash
sudo systemd-machine-id-setup
sudo dbus-uuidgen - ensure
cat /etc/machine-id
~~~  
    - 위와 같은 명령을 실행했을 때 16진수 형태의 GUID 값이 표시되면 정상적으로 파일이 만들어진 것!  

2. `x11-apps`패키지와 `X Window System` 기본 서체를 설치  
~~~bash
sudo apt -y install x11-apps xfonts-base xfonts-100dpi xfonts-75dpi xfonts-cyrillic dbus-x11
~~~  

3. vcxsrv 서버 설정을 현재 세션에서 사용하도록 구성하고 쉘을 다시 시작  
~~~bash  
export DISPLAY=:0  
~~~  

4. .bashrc 파일에 위의 설정을 적용한 뒤 저장  
~~~bash  
vim ~/.bashrc  
~~~  
    - `.bashrc`파일 제일 끝에 "export DISPLAY=:0" 추가하고 저장해주기  

5. vcxsrv 서버의 실행을 확인한 뒤 `xeyes` 명령을 친 뒤, 눈 모양의 위젯 확인  

<br/>

📌 __주요 응용프로그램 설치 및 설정(주황색은 내가 설치한 것)__  
📍 Firefox (인터넷 브라우저)  
~~~bash
sudo apt -y install firefox
firefox&
~~~  

📍 <span style="color: orange">Nautilus(리눅스 기본 파일 관리자), File Roller(압축 관리 프로그램)</span>  
~~~bash
sudo apt -y install nautilus file-roller
nautilus&
~~~  

📍 <span style="color: orange">Gnome Terminal</span>  
~~~bash
sudo apt -y install gnome-terminal
gnome-terminal&  
~~~  

📍 한글 표시와 한국어 Locale 설정  
~~~bash
sudo apt -y install language-pack-ko
sudo locale-gen ko_KR.UTF-8
sudo apt -y install fonts-unfonts-core fonts-unfonts-extra fonts-baekmuk fonts-nanum fonts-nanum-coding fonts-nanum-extra
~~~  

📍 Pinta(그림판같은 것)  
~~~bash
sudo apt -y install pinta
pinta&
~~~

📍 Atom  
~~~bash
sudo add-apt-repository ppa:webupd8team/atom
sudo apt update
sudo apt install atom
atom&
~~~
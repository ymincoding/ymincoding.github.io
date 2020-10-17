---
layout: post
title: "[Linux]Text Editor 명령어 정리(vi, emacs)"
description: >
    Linux Text Editor중 가장 많이 쓰이는 vi와 emacs 명령어 정리
author: Yunmin Cho
tags: [Linux]
category: [Linux]
---

📌__vi 텍스트 에디터__  
- 'view'의 vi를 따온 대표적인 Linux Text Editor  
- vi는 `command mode`와 `insert mode` 두 가지 모드가 있다.
- Graphical interface로 2가지 버전이 있다. GNOME 시스템을 위한 `gvim`과 KDE 시스템을 위한 `kvim`  
<span style="color: gray">_(*GNOME과 KDE는 Linux의 desktop manager)_</span>  

<br/>

✔ __Starting, Exiting, Reading and Writing Files in vi__  

| Command | Description |  
|------|---|  
| vi myfile | Start __vi__ and edit __myfile__ |  
| vi -r myfile | Start __vi__ and edit __myfile__ in recovery mode from a system crash |  
| :r file2<RET> | Read in __file2__ and insert at current position |  
| :w<RET> | Write out the file |  
| :w myfile<RET> | Write out the file to __myfile__ |  
| :w! file2<RET> | Overwrite __file2__ |  
| :x<RET> or :wq<RET> | Exit __vi__ and write out modified file |  
| :q<RET> | Quit __vi__ |  
| :q!<RET> | Quit __vi__ even thought modifications have not been saved |  

<br/>

✔ __Changing Position in vi__  

| Command | Description |  
|------|---|  
| arrow keys | Use the arrow keys for up, down, left and right; or: |  
| j or <RET> | One line down |  
| k | One line up |  
| h or Backspace | One character left |  
| l or Space | One character right |  
| 0 | Move to beginning of line |  
| $ | Move to end of line |  
| w | Move to beginning of next word |  
| b | Move back to beginning of preceding word |  
| :0 <RET> or 1G | Move to beginning of file |  
| :n <RET> or nG | Move to line n |  
| :$ <RET> or G | Move to last line in file |  
| ^f or PageDown | Move forward one page |  
| ^b or PageUp | Move backward one page |  
| ^l | Refresh and center screen |  


<br/>

✔ __Searching for Text in vi__  

| Command | Description |  
|------|---|  
| /pattern<RET> | Search forward for pattern |  
| n | Move to next occurrence of search pattern |  
| string<RET> | Search backward for pattern |  
| N | Move to previous occurrence of search pattern |  

<br/>

✔ __Changing, Adding and Deleting Text in vi__  

| Command | Description |  
|------|---|  
| a | Append text after cursor; stop upon __Escape__ key |  
| A | Append text at end of current line; stop upon __Escape__ key |  
| i | Insert text before cursor; stop upon __Escape__ key |  
| I | Insert text at beginning of current line; stop upon __Escape__ key |  
| o | Start a new line below current line, insert text there; stop upon __Escape__ key |  
| O | Start a new line above current line, insert text there; stop upon __Escape__ key |  
| r | Replace character at current position |  
| R | Replace text starting with current position; stop upon __Escape__ key |  
| x | Delete character at current position |  
| Nx | Delete __N__ characters, starting at current position |  
| dw | Delete the word at the current position |  
| D | Delete the rest of the current line |  
| dd | Delete the current line |  
| Ndd or dNd | Delete N lines |  
| u | Undo the previous operation |  
| yy | Yank (cut) the current line and put it in buffer |  
| Nyy or yNy | Yank (cut) N lines and put it in buffer |  
| p | Paste at the current position the yanked line or lines from the buffer |  

<br/>

---

<br/>

📌__emacs 텍스트 에디터__  
- 모든 Linux 시스템에서 사용할 수 있지만, 가끔 default로 설치가 안되어있을 수 있다.  
- vi와 달리 1가지 모드만 있다. 그래서 command mode와 같이 특별한 명령을 수행하고 싶으면, `Control Key(Ctrl)` 또는 `META Key`를 이용해야 한다.  

<br/>

✔ __Starting, Exiting, Reading and Writing Files in emacs__  

| Command | Description |  
|------|---|  
| emacs myfile | Start __emacs__ and edit __myfile__ |  
| Ctl-x i | Insert prompted for file at current position |  
| Ctl-x s | Write out the file keeping current name |  
| Ctl-x Ctl-w | Write out the file giving a new name when prompted |  
| Ctl-x Ctl-s | Write out all files currently being worked on and exit |  
| Ctl-x Ctl-c | Exit after being prompted if there any unwritten modified files |  

<br/>

✔ __Changing Position in emacs__  

| Command | Description |  
|------|---|  
| arrow keys | Use the arrow keys for up, down, left and right; or: |  
| Ctl-n | One line down |  
| Ctl-p | One line up |  
| Ctl-f | One character left |  
| Ctl-b | One character right |  
| Ctl-a | Move to beginning of line |  
| Ctl-e | Move to end of line |  
| M-f | Move to beginning of next word |  
| M-b | Move back to beginning of preceding word |  
| M-< | Move to beginning of file |  
| M-x goto-line n | Move to line n |  
| M-> | Move to end of file |  
| Ctl-v or PageDown | Move forward one page |  
| M-v or PageUp | Move backward one page |  
| Ctl-l | Refresh and center screen |  

<br/>

✔ __Searching for Text in emacs__  

| Command | Description |  
|------|---|  
| Ctl-s | Search forward for prompted for pattern, or for next pattern |  
| Ctl-r | Search backwards for prompted for pattern, or for next pattern |  

<br/>

✔ __Changing, Adding and Deleting Text in emacs__  

| Command | Description |  
|------|---|  
| Ctl-o | Insert a blank line |  
| Ctl-d | Delete character at current position |  
| Ctl-k | Delete the rest of the current line |  
| Ctl-_ or Ctl-x u | Undo the previous operation |  
| Ctl-space | Mark the beginning of the selected region; the end will be at the cursor position |  
| Ctl-w | Yank (cut) the current marked region and put it in buffer |  
| Ctl-y | Paste at the current position the yanked line or lines from the buffer |  

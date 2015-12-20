---
layout: page
title: Git을 사용한 버젼 관리
subtitle: Git 구축 및 설정
minutes: 5
---
> ## 학습 목표 {.objectives}
>
> *  `git` 환경설정하고 본인 컴퓨터에 사용한다.
> * `--global` 환경설정 플래그 의미를 이해한다.

처음 Git를 새로운 컴퓨터에 사용할 때, 몇가지 설정이 필요하다. 다음에 Dracula가 새로 구입한 노트북에 환경설정하는 방법이 나와있다:

~~~ {.bash}
$ git config --global user.name "Vlad Dracula"
$ git config --global user.email "vlad@tran.sylvan.ia"
$ git config --global color.ui "auto"
~~~
(드라큘라 정보 대신에 자신의 이름과 전자우편 주소를 사용한다.)

다음 표를 참조해서, 본인이 선호하는 텍스트 편집기로 환경설정을 한다:

| 편집기             | 환경설정 명령어                             |
|:-------------------|:-------------------------------------------------|
| nano               | `$ git config --global core.editor "nano -w"`    |
| Text Wrangler      | `$ git config --global core.editor "edit -w"`    |
| Sublime Text (맥) | `$ git config --global core.editor "subl -n -w"` |
| Sublime Text (윈도우) | `$ git config --global core.editor "'c:/program files/sublime text 2/sublime_text.exe' -w"` |
| Notepad++ (윈도우)    | `$ git config --global core.editor "'c:/program files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`|
| Kate (리눅스)       | `$ git config --global core.editor "kate"`       |
| Gedit (리눅스)      | `$ git config --global core.editor "gedit -s"`   |


Git 명령어는 `git verb` 형식으로 작성되고 `verb` 가 실제로 수행하고자 하는 명령어가 된다. 
상기의 경우 Git에게 다음을 명령한다:

*  자신의 이름과 전자우편 주소
*  출력 결과를 색깔을 넣어 표현
*  선호하는 텍스트 편집기 선정
*  설정 사항을 전역(global)으로 한다. (즉, 모든 프로젝트에 적용)

상기 4개 명령어는 한번만 실행되면 된다: 
`--global` 플래그가 Git에게 해당 컴퓨터에서 실행되는 모든 프로젝트에 적용되도록 일러준다.

언제든지 설정 사항을 다음 명령어로 확인할 수 있다:

~~~ {.bash}
$ git config --list
~~~

원하는 만큼 얼마든지 환경설정을 바꿀 수 있다: 동일한 명령어를 사용해서
다른 편집기 정보와 전자우편주소를 갱신한다.

> ## Proxy {.callout}
>
> 일부 네트워크 환경에서 [proxy](https://en.wikipedia.org/wiki/Proxy_server)를
> 사용할 필요가 있다. 
> 이런 경우에, Git에게 프록시 정보를 일러줄 필요가 있다:
>
> ~~~ {.bash}
> $ git config --global http.proxy proxy-url
> $ git config --global https.proxy proxy-url
> ~~~
>
> 프록시를 비활성화 시키려면, 다음을 사용한다.
>
> ~~~ {.bash}
> $ git config --global --unset http.proxy
> $ git config --global --unset https.proxy
> ~~~

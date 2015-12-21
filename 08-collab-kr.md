---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 협업
minutes: 25
---
> ## 학습 목표 {.objectives}
>
> *  공동 저장소로 푸쉬해서 협업한다.


다음 단계로, 짝을 짖는다. 한 사람이 "소유자"(연습을 시작하는데 사용될 GitHub 저장소 주인)가 되고, 다른 사람이 "협력자"(소유자 저장소를 복제해서 변경을 하는 사람)가 된다.


> ## 혼자 훈련하기 {.callout}
>
> 스스로 학습을 쭉해 왔다면, 
> 두번째 터미널 윈도우를 열고 다른 디렉토리(예를 들어, `/tmp`)로 바꾸어 계속 진행할 수 있다. 
> 두번째 윈도우가 여러분의 협력자를 나타내고, 다른 컴퓨터에서 작업하고 있다.
> GitHub 접근권한을 다른 사람에게 줄 필요는 없다. 
> 왜냐하면 두 '파트너' 모두 여러분이기 때문이다.

소유자가 협력자에게 접근권한을 부여할 필요가 있다. 
GitHub에서 오른쪽에 'setting' 버튼을 클릭해서 협력자 사용자이름을 입력한다.

![GitHub에 협력자 추가](fig/github-add-collaborators.png)


협력자는 로컬 컴퓨터에서 해당 프로젝트 작업을 수행할 필요가 있다.
`cd` 명령어로 또 다른 디렉토리로 가서 (`ls` 명령어로 `planets` 폴더를 볼 수 없다.), 소유자 저장소 사본을 만든다:

~~~ {.bash}
$ git clone https://github.com/vlad/planets.git
~~~

'vlad'를 소유자 사용자이름(저장소를 소유하고 있는 사람)으로 바꾼다.

`git clone` 명령어는 원격 저장소와 동일한 새로운 로컬 사본을 생성한다.

![저장소 복제를 생성한 후](fig/github-collaboration.svg)

이제 새로운 협력자가 자신의 저장소에 변경사항을 만들 수 있다:

~~~ {.bash}
$ cd planets
$ nano pluto.txt
$ cat pluto.txt
~~~
~~~ {.output}
It is so a planet!
~~~
~~~ {.bash}
$ git add pluto.txt
$ git commit -m "Some notes about Pluto"
~~~
~~~ {.output}
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
~~~

그리고, 변경사항을 GitHub에 푸쉬한다:

~~~ {.bash}
$ git push origin master
~~~
~~~ {.output}
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 306 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/vlad/planets.git
   9272da5..29aba7c  master -> master
~~~

주목할 점은 `origin` 이라는 원격 저장소를 생성할 필요는 없다:
저장소를 복제(clone)할때 사용한 이름을 Git이 자동으로 사용해서 수행한다. 
(수작업으로 원격 설정을 할 때, 앞에서 왜 `origin` 이름을 사용한 것이 현명한 선택인 이유다.)

이제 우리의 컴퓨터에 GitHub 원본 저장소의 변경사항을 다운로드할 수 있다:

~~~ {.bash}
$ git pull origin master
~~~
~~~ {.output}
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Updating 9272da5..29aba7c
Fast-forward
 pluto.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 pluto.txt
~~~

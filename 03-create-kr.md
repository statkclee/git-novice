---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 저장소 생성
minutes: 10
---
> ## 학습목표 {.objectives}
> 
> *   로컬 컴퓨터에 Git 저장소를 생성한다.

Git 환경설정이 완료되면, Git를 사용할 수 있다. 작업을 위해서 디렉토리를 생성하고 나서,
해당 디렉토리로 이동한다.

~~~ {.bash}
$ mkdir planets
$ cd planets
~~~
그리고 나서, `planets`을 [저장소(repository)](reference.html#repository)로 만든다 &mdash; 저장소는 Git이 파일에 대한 버젼정보를 저장하는 장소다:

~~~ {.bash}
$ git init
~~~
`ls`를 사용해서 디렉토리 내용을 살펴보면, 변한 것이 아무것도 없는 것처럼 보인다:

~~~ {.bash}
$ ls
~~~
하지만, 모든 것을 보여주는 `-a` 플래그를 추가하면 , Git가 `planets` 디렉토리 내부에 `.git` 로 불리는 숨겨진 디렉토리를 생성한 것을 볼 수 있다:

~~~ {.bash}
$ ls -a
~~~
~~~ {.output}
.	..	.git
~~~

Git은 `.git`이라는 특별한 하위 디렉토리에 프로젝트에 대한 정보를 저장한다. 
만약 `.git`를 삭제하면, 프로젝트 이력을 모두 잃어버리게 된다.

모든 것이 제대로 설정되었는지를 확인을 하려면,
Git에게 다음과 같이 프로젝트 상태를 확인 명령어를 던진다:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~

> ## Git 저장소를 생성할 장소 {.challenge}
>
> 드라큘라는 `plantes` 프로젝트와 관련된, 새로운 프로젝트 `moons` 를 시작한다.
> 늑대인간의 걱정에 불구하고, Git 저장소 내부에 또다른 Git 저장소를 생성하려고 
> 다음 순서로 명령어를 입력해 나간다:
> 
> ~~~ {.bash}
> cd             # 홈 디렉토리로 되돌아 간다.
> mkdir planets  # 신규 디렉토리 planets를 생성한다.
> cd planets     # planets 디렉토리로 들어간다.
> git init       # planet 디렉토리에 Git 저장소를 생성한다.
> mkdir moons    # 하위 디렉토리 planets/moons를 생성한다.
> cd moons       # planets/moons로 들어간다.
> git init       # Git 저장소를 moons 하위디렉토리에 생성한다.
> ~~~
> 
> 이렇게 하는 것이 왜 나쁜 생각일까?
> 드라큘라는 마지막 `git init` 명령어를 "실행취소(undo)"할  수 있을까?

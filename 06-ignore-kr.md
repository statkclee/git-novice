---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 관리에서 제외
minutes: 5
---
> ## 학습 목표 {.objectives}
> 
> *   특정 파일을 무시하여 관리에서 제외하도록 Git 환경설정.
> *   파일을 무시하는 것이 왜 유용한지 설명한다.

만약 Git가 추적하기 않았으면 하는 파일이 있다면 어떨까요? 편집기에서 자동 생성되는 백업파일 혹은 자료 분석 중에 생성되는 중간 임시 파일이 좋은 예가 된다. 몇개 마루타 더미(dummy) 파일을 생성하자:


~~~ {.bash}
$ mkdir results
$ touch a.dat b.dat c.dat results/a.out results/b.out
~~~

그려면 Git은 다음을 보여준다:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	a.dat
#	b.dat
#	c.dat
#	results/
nothing added to commit but untracked files present (use "git add" to track)
~~~

벼젼 제어 아래 이런 파일을 놓는 것은 디스크 공간 낭비다.
더 좋은 않는 것은, 이런 파일을 모두 관리목록에 넣는 것이 실제적으로 중요한 변경사항을 관리하는데 집중하지 못하게 한다는 것이다.
그래서 Git에게 중요하지 않는 이런 파일을 무시하게 일러주다.

`.gitignore`라는 프로젝트 루트 디렉토리에 파일을 생성해서 무시할 것을 명기함으로써 해당작업을 수행한다:

~~~ {.bash}
$ nano .gitignore
$ cat .gitignore
~~~
~~~ {.output}
*.dat
results/
~~~

상기 패턴은 `.dat` 확장자를 갖는 임의 파일과 `results` 디렉토리에 있는 모든 것을 무시한다. 
(하지만, 이들 파일 중 일부가 이미 추적되고 있다면, Git은 계속 추적한다.)

`.gitignore` 파일을 생성하자마자, `git status` 출력결과는 훨씬 깨끗해졌다:


~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	.gitignore
nothing added to commit but untracked files present (use "git add" to track)
~~~

이제 Git가 알아차리는 유일한 것은 새로 생성된 `.gitignore` 파일이 된다. 
우리는 이들 파일을 추적하여 관리하지 않는다고 생각할 수도 있지만, 우리와 저장소를 공유하고 있는 다른 모든 사람도 우리가 추적관리하지 않는 동일한 것을 무시하고 싶을 것이다. `.gitignore` 를 추가하고 커밋하자:

~~~ {.bash}
$ git add .gitignore
$ git commit -m "Add the ignore file"
$ git status
~~~
~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

보너스로, `.gitignore`는 실수로 추적하고 싶지 않는 파일이 저장소에 추가되는 것을 피할 수 있게 돕는다:

~~~ {.bash}
$ git add a.dat
~~~
~~~ {.output}
The following paths are ignored by one of your .gitignore files:
a.dat
Use -f if you really want to add them.
fatal: no files added
~~~

만약 `.gitignore` 설정에 우선해서 파일을 추가하려면, `git add -f`를 사용해서 강제로 Git에 파일을 추가할 수 있다. 추적관리되지 않는 파일의 상태를 항상 보려면 다음을 사용한다:


~~~ {.bash}
$ git status --ignored
~~~
~~~ {.output}
# On branch master
# Ignored files:
#  (use "git add -f <file>..." to include in what will be committed)
#
#        a.dat
#        b.dat
#        c.dat
#        results/

nothing to commit, working directory clean
~~~

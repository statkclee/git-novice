---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 이력 탐색
minutes: 25
---
> ## 학습 목표 {.objectives}
>
> *   Git 커밋 번호를 식별하고 사용한다.
> *   다양한 추적 파일버젼을 비교한다.
> *   옛 버젼 파일을 복원한다.

다른 단계에서 무엇을 변경했는지 알고자 한다면, `git diff`를 다시 사용한다. 
하지만 이전 버젼은 `HEAD~1`, `HEAD~2`, 등등 표기법으로 사용한다:

~~~ {.bash}
$ git diff HEAD~1 mars.txt
~~~
~~~ {.output}
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~
~~~ {.bash}
$ git diff HEAD~2 mars.txt
~~~
~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

이런 방식으로, 
연쇄 커밋 사슬을 구성할 수 있다. 
가장 최근 사슬의 끝값은 `HEAD`로 참조된다; 
`~` 표기법을 사용하여 이전 커밋을 참조할 수 있다. 
그래서 `HEAD~1`("head 마이너스 1"으로 읽는다.)은 "바로 앞선 커밋"을 의미하고, 
`HEAD~123`은 지금 있는 위치에서 123번째 이전 수정으로 간다는 의미가 된다.

커밋된 것을 `git log` 명령어로 화면에 뿌려주는 숫자와 문자로 구성된 긴 문자열을 사용하여 참조할 수도 있다. 변경사항에 대해서 중복되지 않는 ID로 "중복되지 않는(unique)"의 의미는 정말 유일하다는 의미다: 
특정 컴퓨터에 있는 임의 파일 집합에 대한 모든 변경사항은 중복되지 않는 40-문자 식별자가 붙어있다. 
첫번째 커밋은 ID로 f22b25e3233b4645dabd0d81e651fe074bd8e73b 이 주어졌다. 
그래서 다음과 같이 시도하자:

~~~ {.bash}
$ git diff f22b25e3233b4645dabd0d81e651fe074bd8e73b mars.txt
~~~
~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

올바든 정답이지만, 
난수 40-문자로 된 문자열을 타이핑하는 것은 매우 귀찮은 일이다. 
그래서 Git 앞의 몇개 문자만으로도 사용할 수 있게 했다:

~~~ {.bash}
$ git diff f22b25e mars.txt
~~~
~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

좋았어요! 
파일에 변경사항을 저장할 수 있고 변경된 것을 확인할 수 있다. 
어떻게 옛 버젼 파일을 되살릴 수 있을까? 
우연히 파일을 덮어썼다고 가정하자:

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~
~~~ {.output}
We will need to manufacture our own oxygen
~~~

이제 `git status`를 통해서 파일이 변경되었다고 하지만, 
변경사항은 아직 준비영역(Stagin)에 옮겨지지 않은 것으로 확인된다:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   mars.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
~~~

`git checkout` 명령어를 사용해서 과거에 있던 상태로 파일을 돌려 놓을 수 있다:

~~~ {.bash}
$ git checkout HEAD mars.txt
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~

이름에서 유추할 수 있듯이, `git checkout` 명령어는 파일 옛 버젼을 확인하고 갖고 나간다. 즉, 되살린다. 
이 경우 `HEAD`에 기록된 가장 최근에 저장된 파일 버젼을 되살린다. 
좀더 오래된 버젼을 되살리고자 한다면, 대신에 커밋 식별자를 사용한다:

~~~ {.bash}
$ git checkout f22b25e mars.txt
~~~

실행 취소를 하는 변경을 하기 *전에** 저장소 상태를 확인하는 커밋 번호를 사용해야 한다는 것을 기억하는 것이 중요하다. 
흔한 실수는 제거하려고 변경하려고 사용한 커밋 번호를 사용하는 것이다. 
아래 예제에서는 커밋 번호가 `f22b25e`인 가장 최신 커밋(`HEAD~1`) 앞의 상태로 다시 되돌리고자 한다:

![Git Checkout](fig/git-checkout.svg)

그래서, 모두 한군데 놓아보자:

> ## 만화로 보는 Git 동작 방식. {.callout}
> ![http://figshare.com/articles/How_Git_works_a_cartoon/1328266](fig/git_staging.svg)

> ## 일반적인 사례를 단순화 {.callout}
>
>`git status` 출력 결과를 주의 깊이 읽게 되면, 힌트가 포함된 것을 보게 된다:
>
> ~~~ {.bash}
> (use "git checkout -- <file>..." to discard changes in working directory)
> ~~~
>
> 출력 결과가 말해주듯이, 
> 버젼 식별자 없는 `git checkout` 명령어가 `HEAD`에 저장된 상태로 파일을 되돌린다. 
> 이중 대쉬 `--`는 명령어 그자체로부터 되살리려는 파일 이름을 구별하는데 필요하다: 
> 이중 대쉬가 없다면, Git는 파일 이름을 커밋 식별자로 사용한다.

파일이 하나씩 하나씩 옛 상태로 되돌린다는 사실이 사람들이 작업을 조직하는 방식에 변화를 주는 경향이 있다. 
모든 것이 하나의 큰 문서로 되어있다면, 나중에 결론부분에 변경사항을 실행취소하지 않고, 소개부분에 변경을 다시 되돌리기가 쉽지 않다(하지만 불가능하지는 않다). 
다른 한편으로 만약 소개부분과 결론부분이 다른 파일에 저장되어 있다면, 
시간 앞뒤로 이동하기가 훨씬 쉽다.

> ## 파일 이전 버젼 복구하기 {.challenge}
>
> 정훈이가 몇주동안 작업한 파이썬 스크립트에 변경을 했고,
> 오늘 아침 정훈이가 작업한 변경사항이 스크립트를 "망가 먹어서" 더이상 실행이 되지 않는다.
> 복도 없이, 버그를 고치는데 1시간 이상 소모했다...
>
> 다행스럽게도, Git을 사용한 프로젝트 버젼을 추적하고 있었다!
> 다음 아래 명령어 중 어떤 것이 `data_cruncher.py`로 불리는 파이썬 스크립트 가장 최근 버젼을 
> 복구하게 할까요?
>
> 1. 
>
>     ~~~
>     $ git checkout HEAD
>     ~~~
> 2. 
>
>     ~~~
>     $ git checkout HEAD data_cruncher.py
>     ~~~
> 3. 
>
>     ~~~
>     $ git checkout HEAD~1 data_cruncher.py
>     ~~~
> 4. 
>
>     ~~~
>     $ git checkout <unique ID of last commit> data_cruncher.py
>     ~~~
> 5. Both 2 & 4

---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 변경사항 추적
minutes: 20
---
> ## 학습 목표 {.objectives}
> 
> *   파일 한개 혹은 다수 파일에 대해서 변경-추가-커밋(modify-add-commit) 주기를 수행한다.
> *   각 Git 커밋 작업흐름 단계별로 정보가 어디에 저장되는지 설명한다.

전진기지로서 화성의 적합성에 관한 기록을 담고 있는 `mars.txt` 파일을 생성한다. 
(파일 편집을 위해서 `nano` 편집기를 사용한다; 원하는 어떤 편집기를 사용해도 된다. 
특히, 앞에서 전역으로 설정한 `core.editor`가 될 필요도 없다.)

~~~ {.bash}
$ nano mars.txt
~~~

`mars.txt` 파일에 다음 텍스트를 타이핑한다:

~~~ {.output}
Cold and dry, but everything is my favorite color
~~~

`mars.txt` 파일은 이제 한 줄을 포함하고 있고, 다음 명령어로 내용을 확인할 수 있다:

~~~ {.bash}
$ ls
~~~
~~~ {.output}
mars.txt
~~~
~~~ {.bash}
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
~~~

다시 한번 프로젝트의 상태를 확인하고자 하면, 
새로운 파일이 인지되었다고 Git이 일러준다:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	mars.txt
nothing added to commit but untracked files present (use "git add" to track)
~~~

"untracked files" 메시지가 의미하는 것은 Git가 추적하고 있지 않는 파일 하나가 디렉토리에 있다는 것이다. 
`git add`를 사용해서 Git에게 추적관리하라고 일러준다:

~~~ {.bash}
$ git add mars.txt
~~~

그리고 나서, 올바르게 처리되었는지 확인한다:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#	new file:   mars.txt
#
~~~

이제 Git은 `mars.txt` 파일을 추적할 것이라는 것을 알고 있지만, 
커밋으로 아직 저장소에는 어떤 변경사항도 기록되지 않았다. 
이를 위해서 명령어 하나 더 실행할 필요가 있다:

~~~ {.bash}
$ git commit -m "Start notes on Mars as a base"
~~~
~~~ {.output}
[master (root-commit) f22b25e] Start notes on Mars as a base
 1 file changed, 1 insertion(+)
 create mode 100644 mars.txt
~~~

`git commit`을 실행할 때, 
Git은 `git add`를 사용해서 저장하려고 하는 모든 대상을 받아서 
`.git` 디렉토리 내부에 영구적으로 사본을 저장한다. 
이 영구 사본을 [커밋(commit)](reference.html#commit)
(혹은 [수정(revision)](reference.html#revision))이라고 하고, 
짧은 식별자는 `f22b25e`이다. (여러분의 커밋번호의 짧은 식별자는 다를 수 있다.)

`-m` ("message"를 위미) 플래그를 사용해서 나중에 무엇을 왜 했는지 기억에 도움이 될 수 있는 주석을 기록한다. 
`-m`옵션 없이 `git commit`을 실행하면, 
Git는 `nano`(혹은 처음에 설정한 다른 편집기)를 실행해서 좀더 긴 메시지를 작성할 수 있다.

[좋은 커밋 메시지(Good commit messages)][commit-messages] 작성은 
커밋으로 만들어진 간략한 변경사항 요약으로 시작된다.
만약 좀더 상세한 사항을 남기려면,
요약줄 사이에 빈줄을 추가하고 추가적인 내역을 적는다.

이제 `git status`를 시작하면:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

모든 것이 최신 상태라고 보여준다. 
최근에 작업한 것을 알고자 한다면, 
`git log`를 사용해서 프로젝트 이력을 보여주도록 Git에게 명령어를 보낸다:

~~~ {.bash}
$ git log
~~~
~~~ {.output}
commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Start notes on Mars as a base
~~~

`git log`는 시간 역순으로 저장소의 모든 변경사항을 나열한다.
각 수정사항 목록은 전체 커밋 식별자(앞서 `git commit` 명령어로 출력한 짧은 문자와 동일하게 시작), 
수정한 사람, 언제 생성되었는지, 커밋을 생성할 때 Git에 남긴 로그 메시지가 포함된다. 

> ## 내가 작성한 변경사항은 어디있나? {.callout}
>
> 이 시점에서 `ls` 명령어를 다시 실행하면, 
> `mars.txt` 파일만 덩그러니 보게 된다. 
>  왜냐하면, Git이 앞에서 언급한 `.git` 특수 디렉토리에 파일 변경 이력 정보를 저장했기 때문이다.
> 그래서 파일 시스템이 뒤죽박죽되지 않게 된다. 
> (따라서, 옛 버젼을 실수로 편집하거나 삭제할 수 없다.)

이제 드라큘라가 이 파일에 정보를 더 추가했다고 가정하자. 
(다시 한번 `nano`편집기로 편집하고 나서 `cat`으로 파일 내용을 살펴본다. 
다른 편집기를 사용할 수도 있고, `cat`으로 파일 내용을 꼭 볼 필요도 없다.)

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
~~~

`git status`를 실행하면, 
Git이 이미 알고 있는 파일이 변경되었다고 일러준다:

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

마지막 줄이 중요한 문구다: 
"no changes added to commit". 
`mars.txt` 파일을 변경했지만, 아직 Git에게는 변경을 사항을 저장하려고 하거나 (`git add`로 수행),
저장소에 저장하라고  (`git commit`로 수행) 일러주지도 않았다. 
이제 행동에 나서보자.
저장하기 전에 변경사항을 항상 검토하는 것은 좋은 습관이다.
`git diff`를 사용해서 작업 내용을 두번 검증한다. 
`git diff`는 현재 파일의 상태와 가장 최근에 저장된 버젼의 차이를 보여준다:

~~~ {.bash}
$ git diff
~~~
~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..315bf3a 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,2 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
~~~

출력 결과가 암호같은데 이유는 한 파일이 주어졌을 때 다른 파일 하나를 어떻게 재구성하는지를 일러주는 `patch`와 편집기 같은 도구를 위한 일련의 명령어라서 그렇다.
만약 해당 내역을 조각내서 쪼개다면:

1.  첫번째 행은 Git이 신규 파일과 옛 버젼 파일을 비교하는 유닉스 `diff` 명령어와 유사한 출력결과를 생성하고 있다.
2.  두번째 행은 정확하게 Git이 파일 어느 버젼을 비교하는지 일러준다; 
      `df0654a`와 `315bf3a`은 해당 버젼에 대해서 중복되지 않게 컴퓨터가 생성한 표식이다.
3.  세번째와 네번째 행은 변경되는 파일 명칭을 다시한번 보여주고 있다.      
4.  나머지 행이 가장 흥미롭다. 실제 차이가 나는 것과 어느 행에서 발생했는지 보여준다. 
     특히 첫번째 열의 `+` 기호는 어디서 행이 추가 되었는지 보여준다.

변경사항 검토후에, 변경사항을 커밋(commit)하자.

~~~ {.bash}
$ git commit -m "Add concerns about effects of Mars' moons on Wolfman"
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

이럴 수가, `git add`을 먼저 하지 않아서 Git이 커밋을 할 수 없다. 
고쳐봅시다:

~~~ {.bash}
$ git add mars.txt
$ git commit -m "Add concerns about effects of Mars' moons on Wolfman"
~~~
~~~ {.output}
[master 34961b1] Add concerns about effects of Mars' moons on Wolfman
 1 file changed, 1 insertion(+)
~~~

실제로 무엇을 커밋하기 전에 커밋하고자하는 파일을 먼저 추가하라고 Git이 주문하는데, 
이유는  한번에 모든것을 커밋하지 싶지 않을수도 있기 때문이다. 
예를 들어, 작성하고 있는 논문에 지도교수 논문을 일부 인용하여 추가한다고 가정하자. 
논문 중간에 인용되는 추가부분과 상응되는 참고문헌을 커밋하고는 싶지만,
결론 부분을 커밋하고는 싶지 *않다.* (아직 결론이 완성되지 않았다.)

이런 점을 고려해서, 
Git은 특별한 *준비 영역(staging)*이 있어서 현재 [변경부분(change set()](reference.html#change-set)을 추가는 했으나 아직 커밋하지 않는 것을 준비 영역에서 추적하고 있다. 

> ## 준비 영역(Staging area) {.callout}
> 프로젝트 기간 동안에 걸쳐 발생된 변경사항에 대해 스냅사진을 찍는 것으로 Git을 바라보면,
> `git add` 명령어는 *무엇*이 스냅사진(준비영역에 놓는 것)에 들어갈지 명세하고,
> `git commit` 명령어는 *실제로* 스탭사진을 찍는 것이다.
> 만약 `git commit`을 타이핑할 때 준비된 어떤 것도 없다면,
> Git이 `git commit -a` 혹은 `git commit --all` 명령어 사용을 재촉한다.
> 사진을 찍으려고 *모두* 모이세요 하는 것과 같다.
> 하지만, 준비영역에 추가할 것을 명시적으로 하는 것이 항상 좋다.
> 왜냐하면 커밋을 했는데 잊은 것이 있을 수도 있기 때문이다.
> (스냅사진으로 돌아가서, `-a` 옵션을 사용했기 때문에 스냅사진에 들어갈 항목을 불완전하게
작성했을 수도 있다!)
> 수작업으로 준비영역에 올리거나,
> 원하는 것보다 많은 것을 올렸다면 "git undo commit"을 찾아보라.
![The Git Staging Area](fig/git-staging-area.svg)

파일 변경사항을 편집기에서 준비 영역으로, 그리고 장기 저장소로 옮기는 것을 살펴보자. 
먼저, 파일에 행 하나를 더 추가한다:

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~
~~~ {.bash}
$ git diff
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

지금까지 좋다. 
파일의 끝에 행을 하나 추가했다(첫 열에 `+`이 보인다). 
이제, 준비영역에 변경 사항을 놓고, `git diff` 명령어가 보고하는 것을 살펴보자:

~~~ {.bash}
$ git add mars.txt
$ git diff
~~~

출력결과가 없다. 
Git이 일러줄 수 있는 것은 영구히 저장되는 것과 현재 디렉토리에 작업하고 있는 것에 차이가 없다는 것이다. 
하지만, 다음과 같이 명령어를 친다면:

~~~ {.bash}
$ git diff --staged
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

마지막으로 커밋된 변경사항과 준비 영역(Staging)에 있는 것과 차이를 보여준다. 
변경사항을 저장하자:

~~~ {.bash}
$ git commit -m "Discuss concerns about Mars' climate for Mummy"
~~~
~~~ {.output}
[master 005937f] Discuss concerns about Mars' climate for Mummy
 1 file changed, 1 insertion(+)
~~~

현재 상태를 확인하자:

~~~ {.bash}
$ git status
~~~
~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

그리고 지금까지 작업한 이력을 살펴보자:

~~~ {.bash}
$ git log
~~~
~~~ {.output}
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:14:07 2013 -0400

    Discuss concerns about Mars' climate for Mummy

commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:07:21 2013 -0400

    Add concerns about effects of Mars' moons on Wolfman

commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Start notes on Mars as a base
~~~
요약하면, 
변경사항을 저장소에 추가하고자 할 때, 
먼저 변경된 파일을 준비 영역(Staging)에 `git add` 명령어로 추가하고 나서, 
준비 영역의 변경사항을 저장소에 `git commit` 명령어로 최종 커밋한다:


![Git 커밋 작업흐름](fig/git-committing.svg)


> ## 변경사항을 Git에 커밋하기 {.challenge}
>
> 본인 로컬 컴퓨터 Git 저장소에 아래 다음 명령어 중에서 어떤 것이 `myfile.txt` 파일 변경사항을 저장할까?
>
> 1. 
>
>     ~~~
>     $ git commit -m "my recent changes"
>     ~~~
> 2. 
>
>     ~~~
>     $ git init myfile.txt
>     $ git commit -m "my recent changes"
>     ~~~
> 3. 
>
>     ~~~
>     $ git add myfile.txt
>     $ git commit -m "my recent changes"
>     ~~~
> 4. 
>
>     ~~~
>     $ git commit -m myfile.txt "my recent changes"
>     ~~~

> ## `bio` 저장소 {.challenge}
>
> `bio`라는 새로운 Git 저장소를 본인 로컬 컴퓨터에 생성한다.
> `me.txt`라는 파일로 본인에 대한 3줄 이력서를 작성한다.
> 변경사항을 커밋한다.
> 그리고 나서 한줄을 바꾸고, 네번째 줄을 추가하고 나서,
> 원래 상태와 갱신된 상태의 차이를 화면에 출력한다.

[commit-messages]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

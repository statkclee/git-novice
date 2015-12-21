---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 충돌
minutes: 15
---
> ## 학습 목표 {.objectives}
>
> *   충돌이 무엇이고, 언제 생기는지를 설명한다.
> *   병합(merge)로부터 생기는 충돌을 해결한다.

사람들이 병렬로 작업을 할 수 있게 됨에 따라, 
누군가 다른 사람 작업영역을 발을 들여 넣을 가능성이 있다.
혼자서 작업할 경우에도 이런 현상이 발생한다: 
소프트웨어 개발을 개인 노트북과 연구실 서버에서 작업한다면, 
각 작업본에 다른 변경사항을 만들 수 있다. 
버젼 제어(version control)가 겹치는 변경사항을 [해결(resolve)](reference.html#resolve)하는 툴을 제공함으로서, 이러한 [충돌(conflicts)](reference.html#conflicts)을 관리할 수 있게 돕는다.

충돌을 어떻게 해소할 수 있는지 확인하기 위해서, 
먼저 파일을 생성하자. 
`mars.txt` 파일은 현재 두 협업하는 사람의 `planets` 저장소 사본에서는 다음과 같이 보인다:

~~~ {.bash}
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~

파트너 사본만 한 줄을 추가하자:

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
This line added to Wolfman's copy
~~~

그리고 나서, 변경사항을 GitHub에 푸쉬하자:

~~~ {.bash}
$ git add mars.txt
$ git commit -m "Adding a line in our home copy"
~~~
~~~ {.output}
[master 5ae9631] Adding a line in our home copy
 1 file changed, 1 insertion(+)
~~~
~~~ {.bash}
$ git push origin master
~~~
~~~ {.output}
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 352 bytes, done.
Total 3 (delta 1), reused 0 (delta 0)
To https://github.com/vlad/planets
   29aba7c..dabb4c8  master -> master
~~~

이제 또다른 파트너가 GitHub에서 갱신(update)하지 *않고*,
사본에 다른 변경사항을 작업한다:

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
We added a different line in the other copy
~~~

로컬 저장소에 변경사항을 커밋할 수 있다:

~~~ {.bash}
$ git add mars.txt
$ git commit -m "Adding a line in my copy"
~~~
~~~ {.output}
[master 07ebc69] Adding a line in my copy
 1 file changed, 1 insertion(+)
~~~

하지만 GitHub에는 푸쉬할 수 없다:

~~~ {.bash}
$ git push origin master
~~~
~~~ {.output}
To https://github.com/vlad/planets.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/vlad/planets.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
~~~

![충돌하는 변경사항](fig/conflict.svg)

본인이 작업한 변경사항이 다른 사람이 작업한 변경사항과 중첩되는 것을 Git이 탐지해서, 앞에서 작업한 것을 뭉개지 않도록 정지시킨다.
이제 해야될 작업은 GitHub에서 변경사항을 풀(Pull)해서 가져오고 현재 작업중인 작업본과 [병합(merge)](reference.html#merge)해서 푸쉬한다. 풀(Pull)부터 시작하자:

~~~ {.bash}
$ git pull origin master
~~~
~~~ {.output}
remote: Counting objects: 5, done.        
remote: Compressing objects: 100% (2/2), done.        
remote: Total 3 (delta 1), reused 3 (delta 1)        
Unpacking objects: 100% (3/3), done.
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Auto-merging mars.txt
CONFLICT (content): Merge conflict in mars.txt
Automatic merge failed; fix conflicts and then commit the result.
~~~

`git pull` 수행결과 충돌이 있다고 일러주고, 
해당 파일에 충돌나는 부분을 표시한다:

~~~ {.bash}
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
<<<<<<< HEAD
We added a different line in the other copy
=======
This line added to Wolfman's copy
>>>>>>> dabb4c8c450e8475aee9b14b4383acc99f42af1d
~~~

`<<<<<<<` 다음에 `HEAD`에 있는 본인 변경사항이 나와있다. 
Git이 자동으로 `=======`을 넣어서 충돌나는 변경사항 사이에 구분자로 넣고,
`>>>>>>>`으로 GitHub에서 다운로드된 파일 내용의 마지막을 표시한다. (`>>>>>>>` 표시자 다음에 문자와 숫자로 구성된 문자열로 방금 다운로드한 커밋번호를 식별한다.)

파일을 편집해서 표시자/구분자를 제거하고 변경사항을 일치하는 것은 전적으로 여러분에게 달려있다. 
원하는 무엇이든지 할 수 있다: 
예를 들어, 로컬 저장소의 변경사항을 반영하든, 원격 저장소의 변경사항을 반영하든, 로컬과 원격 저장소의 내용을 대체하는 새로운 것을 작성하든, 혹은 변경사항을 완전히 제거하는 것도 가능하다. 
로컬과 원격 모두 교체해서 다음과 같이 파일이 보이도록 하자:

~~~ {.bash}
$ cat mars.txt
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
We removed the conflict on this line
~~~

병합을 마무리하기 위해서, 
병합으로 생성된 변경사항을 `mars.txt` 파일에 추가하고 커밋한다:

~~~ {.bash}
$ git add mars.txt
$ git status
~~~
~~~ {.output}
# On branch master
# All conflicts fixed but you are still merging.
#   (use "git commit" to conclude merge)
#
# Changes to be committed:
#
#	modified:   mars.txt
#
~~~
~~~ {.bash}
$ git commit -m "Merging changes from GitHub"
~~~
~~~ {.output}
[master 2abf2b1] Merging changes from GitHub
~~~

이제 변경사항을 GitHub에 푸쉬할 수 있다:

~~~ {.bash}
$ git push origin master
~~~
~~~ {.output}
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 697 bytes, done.
Total 6 (delta 2), reused 0 (delta 0)
To https://github.com/vlad/planets.git
   dabb4c8..2abf2b1  master -> master
~~~

Git은 병합하면서 수행한 것을 모두 추적하고 있어서, 
수작업으로 다시 고칠 필요는 없다. 
처음 변경사항을 만든 협력자 프로그래머가 다시 풀하게 되면:

~~~ {.bash}
$ git pull origin master
~~~
~~~ {.output}
remote: Counting objects: 10, done.        
remote: Compressing objects: 100% (4/4), done.        
remote: Total 6 (delta 2), reused 6 (delta 2)        
Unpacking objects: 100% (6/6), done.
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Updating dabb4c8..2abf2b1
Fast-forward
 mars.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
~~~

병합된 파일을 얻게 된다:

~~~ {.bash}
$ cat mars.txt 
~~~
~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
We removed the conflict on this line
~~~

다시 병합할 필요는 없는데, 
다른 누군가 작업을 했다는 것을 Git가 알기 때문이다.

충돌되는 변경사항을 병합하는 버젼제어 기능으로 인해서, 모든 것을 매우 큰 한 파일에 저장하는 대신에 사용자가 프로그램이나 논문을 다중 파일로 쪼개서 작업하는 또다른 이유가 된다. 
또다른 좋은 점도 있다: 특정 파일에 반복되는 충돌이 있을 때마다, 버젼 제어 시스템이 본질적으로 누가 무엇에 책임이 있는지, 작업을 다르게 분업하는 방법을 찾을 수 있도록 명확하게 사용자에게 일러준다.

> ## 본인이 생성한 충돌 해소하기 {.challenge}
>
> 강사가 생성한 저장소를 복제하세요. 
> 저장소에 새 파일을 추가하고, 
> 기존 파일을 변경하세요. 
> (강사가 변경할 기존 파일이 어느 것인지 알려줄 것이다.) 
> 강사의 말에 따라 충돌을 생성하는 연습을 위해서,
> 저장소에서 변경사항을 가져오도록 풀(Pull)하세요. 
> 그리고 충돌을 해소하고 해결해 보세요.

> ## 텍스트 파일이 아닌 충돌 {.challenge}
>
> 버젼 제어 저장소의 이미지 파일이나 혹은 다른 텍스트가 아닌 파일에서 충돌이 발생할 때, 
> Git는 무엇을 하나요?

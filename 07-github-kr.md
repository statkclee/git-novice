---
layout: page
title: Git을 사용한 버젼 관리
subtitle: GitHub 원격작업
minutes: 30
---
> ## 학습 목표 {.objectives}
>
> *   원격 저장소가 무엇인지 그리고 왜 원격 저장소가 유용한지 설명한다.
> *   원격 저장소를 복제(clone)한다.
> *   원격 저장소에서 변경사항을 푸쉬(push)와 풀(pull)한다.

버젼 제어(version control)는 다른 사람과 협업할 때 진정으로 다가온다. 우리는 이미 버젼 제어를 위해 필요한 컴퓨터 대부분을 가졌다. 한가지 빠진 것은 한 저장소에서 다른 저장소로 변경사항을 복사하는 것이다.

Git 같은 시스템은 임의 두 저장소 사이에 작업을 옮길 수 있게 한다.
하지만, 실무에서 다른 사람의 노트북이나 PC보다는 중앙 허브에 웹 방식으로 하나의 원본을 두고 사용하는 것이 가장 쉽다. 
대부분의 프로그래머는 프로그램 마스터 원본을 
[GitHub](http://github.com),
[BitBucket](http://bitbucket.org),
[GitLab](http://gitlab.com/) 호스팅 서비스에 두고 사용한다; 
이번 학습 마지막 부분에서 이러한 접근법의 장점과 단점을 살펴본다.

세상 사람들과 현재 프로젝트에서 변경한 사항을 공유하는 것에서부터 시작해보자. GitHub에 로그인하고 나서, 우측 상단 아이콘을 클릭해서 `planets` 이름으로 신규 저장소를 생성한다:


![Creating a Repository on GitHub (Step 1)](fig/github-create-repo-01.png)

저장소 이름을 "planets"으로 만들고 "Create Repostiory"를 클릭한다:

![Creating a Repository on GitHub (Step 2)](fig/github-create-repo-02.png)

저장소가 생성되자 마자, Git는 URL을 가진 페이지와 사용자가 로컬 저장소 환경설정 방법에 대한 정보를 화면에 출력한다:


![Creating a Repository on GitHub (Step 3)](fig/github-create-repo-03.png)

다음 명령어는 효과적으로 GitHub 서버에서 다음을 자동으로 수행한다:

~~~ {.bash}
$ mkdir planets
$ cd planets
$ git init
~~~

현재 로컬 저장소는 여전히 `mars.txt` 파일에 대한 이전 작업정보를 담고 있다. 
하지만, GitHub의 원격 저장소는 아직 어떠한 파일도 담고 있지는 않다:


![Freshly-Made GitHub Repository](fig/git-freshly-made-github-repo.svg)

다음 단계는 두 저장소를 연결하는 것이다. 
로컬 저장소에 대해서 GitHub 저장소를 [원격(remote)](reference.html#remote) 저장소로 만들어 두 저장소를 연결한다. GitHub에 나온 저장소 홈페이지는 식별하는데 필요한 문자열을 포함하다:


![Where to Find Repository URL on GitHub](fig/github-find-repo-string.png)

SSH에서 HTTPS로 [프로토콜(protocol)](reference.html#protocol)을 변경하려면 'HTTPS' 링크를 클릭한다.


> ## HTTPS vs SSH {.callout}
>
> 부가적인 설정이 필요하지 않아서 여기서는 HTTPS를 사용한다. 
> 워크샵 후에 SSH 접근 설정을 원할지도 모른다. 
> SSH 접근이 좀더 안전하다. 
> [GitHub](https://help.github.com/articles/generating-ssh-keys),
> [Atlassian/BitBucket](https://confluence.atlassian.com/display/BITBUCKET/Set+up+SSH+for+Git), 
> [GitLab](https://about.gitlab.com/2014/03/04/add-ssh-key-screencast/)에 훌륭한 지도서 중 하나를 따라하는 것도 좋다.
> GitLab은 온라인 동영상도 제공한다.

![Changing the Repository URL on GitHub](fig/github-change-repo-string.png)

웹 브라우져에서 URL을 복사하고 나서, 로컬 컴퓨터 `planets` 저장소로 가서 다음 명령어를 실행한다:


~~~ {.bash}
$ git remote add origin https://github.com/vlad/planets.git
~~~

Vlad가 아니고 여러분 저장소의 URL을 사용했는지 확인한다. 
유일한 차이점은 `vlad` 대신에 여러분의 사용자이름(username)이다:

`git remote -v` 실행해서 명령어가 제대로 작동했는지 확인한다:

~~~ {.bash}
$ git remote -v
~~~
~~~ {.output}
origin   https://github.com/vlad/planets.git (push)
origin   https://github.com/vlad/planets.git (fetch)
~~~

`origin` 이름이 원격 저장소에 대한 로컬 별명이다. 
원한다면 다른 명칭을 사용할 수도 있지만, `origin` 이름이 가장 일반적인 선택이다.

별명이 `origin`으로 설정되면, 
다음 명령어가 변경사항을 로컬 저장소에서 GitHub 원격 저장소로 밀어 넣어 푸쉬(push)한다:

~~~ {.bash}
$ git push origin master
~~~
~~~ {.output}
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 821 bytes, done.
Total 9 (delta 2), reused 0 (delta 0)
To https://github.com/vlad/planets
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
~~~

> ## 프록시(Proxy) {.callout}
>
> 만약 연결된 네트워크가 프록시를 사용한다면, 
> 오류 메시지로 "Could not resolve hostname"으로 마지막 명령어가 실패할 가능성이 있다. 
> 이 문제를 해결하기 위해서, 프록시에 대한 정보를 Git에 전달할 필요가 있다:
>
> ~~~ {.bash}
> $ git config --global http.proxy http://user:password@proxy.url
> $ git config --global https.proxy http://user:password@proxy.url
> ~~~
>
> 프록시를 사용하지 않는 또다른 네트워크에 연결될 때, 
> Git에게 프록시 기능을 사용하지 않도록 다음 명령어를 사용하여 일러준다:
>
> ~~~ {.bash}
> $ git config --global --unset http.proxy
> $ git config --global --unset https.proxy
> ~~~

> ## 비밀번호 관리자(password manager) {.callout}
>
> 운영체제에 비밀번호 관리자가 설정되어 있다면, 
> 사용자이름(username)과 비밀번호(passord)가 요구될 때, 
> `git push` 명령어가 이를 사용하려 한다. 
> 비밀번호 관리자를 사용하는 대신에, 
> 터미널에서 사용자이름과 비밀번호를 입력하려면, 
> 다음과 같이 타이핑한다:
>
> ~~~ {.bash}
> $ unset SSH_ASKPASS
> ~~~
>
> 디폴트 기본설정하기 위해서는 `~/.bashrc` 끝에 상기 명령어를 추가하면 된다.

이제 로컬 저장소와 원격 저장소는 다음과 같은 상태가 된다:

![GitHub Repository After First Push](fig/github-repo-after-first-push.svg)

> ## '-u' 플래그(flag) {.callout}
>
> Git 문서에서 `git push`과 함께 사용되는 `-u` 옵션을 볼 수 있다.
> 중급 학습에서 다루는 개념과 연관되어서 여기서는 넘어가도록 한다.

또한, 원격 저장소에서 로컬 저장소를 변경사항을 풀(pull)해서 가져올 수도 있다:

~~~ {.bash}
$ git pull origin master
~~~
~~~ {.output}
From https://github.com/vlad/planets
 * branch            master     -> FETCH_HEAD
Already up-to-date.
~~~

이 경우 가져오기 하는 풀(pull)은 아무런 결과가 없는데, 이유는 두 저장소가 이미 동기화가 되어서다. 
하지만, 만약 누군가 GitHub 저장소에 변경사항을 푸쉬했다면, 상기 명령어는 변경된 사항을 로컬 저장소로 다운로드한다.

> ## GitHub 시간도장(Timestamp) {.challenge}
>
> GitHub에 원격저장소를 생성하라.
> 클론하고, 파일을 추가하고, 변경사항을 GitHub에 푸쉬하고 나서,
> GitHub변경사항에 대한 [시간도장(timestamps)](reference.html#timestamp)을 살펴본다. 
> GitHub이 시간정보를 어떻게 기록하는가? 왜 그런가?

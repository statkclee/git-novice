---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 자동화된 버젼제어
minutes: 5
---
> ## 학습 목표 {.objectives}
>
> *   자동화된 버젼제어 시스템 장점을 이해한다.
> *  Git 동작방법 기본을 이해한다.

누군가 무엇을 했는지, 언제 했는지를 추적하기 위해서, 버젼제어를 어떻게 사용할 수 있는지 탐색해보자.
다른 사람과 협업을 하지 않더라도, 자동화된 버젼제어가 다음 상황보다 훨씬 더 낫다:

[![Piled Higher and Deeper by Jorge Cham, http://www.phdcomics.com](fig/phd101212s.gif)](http://www.phdcomics.com)

"Piled Higher and Deeper" by Jorge Cham, http://www.phdcomics.com

이전에 상기와 같은 상황에 처했었다: 같은 문서에 대해서 거의 동일한 다수 버젼을 관리하는 것은 우수워 보인다.
일부 워드프로세서가 이런 상황을 좀더 잘 처리하도록 하는 기능이 있다. 예를 들어, 마이크로소프트 워드 "변경사항 추적(Track Changes)" 혹은
구글 닥스(Google Docs)의 버젼 이력이 그것이다.

버젼제어 시슽메은 문서의 기본 버젼으로 시작하고 나서, 각 단계마다 변경한 이력을 저장한다.
테이프로 생각하면 쉽다: 테이프를 되감으면, 문서 시작한 지점으로 가고, 각 변경사항을 다시 돌리면 가장 최근 버젼이 된다.

![변경사항이 순차적으로 저장됨](fig/play-changes.svg)

변경사항을 문서 그자체로부터 떨어진 것으로 생각하면,
동일 기반 문서에 다른 변경사항을 "재생(playback)"하고, 다른 문서 버젼을 관리하는 것으로 간주할 수 있다.
예를 들어, 사용자 두명이 같은 문서에 독립적인 변경 작업을 수행할 수 있다.

![다른 버젼이 저장될 수도 있음](fig/versions.svg)

만약 충돌나지 않으면, 심지어 동일 문서에서 두가지 변경사항을 작업할 수도 있다.

![Multiple versions can be merged](fig/merge.svg)

버젼제어 시스템은 사용자를 대신해서 변경사항을 기록하고,
파일 버젼을 생성하고 파일병합하는데 유용한 도구다.
버젼제어 시스템은 어떤 변경사항을 다음 버젼에 반영([커밋(commit)](reference.html#commit)으로 불림)할지 결정하는 할 수 있게 하고,
커밋에 관한 유용한 메타정보를 보관한다.
특정 프로젝트와 프로젝트 메타정보에 대한 완전한 커밋이력은 
[저장소(repository)](reference.html#repository)에 보관된다.
저장소는 협업하는 여러 동료 컴퓨터에 걸쳐 동기화될 수 있다.

> ## 버젼제어 시스템의 오랜 역사 {.callout}
>
> 자동화된 버젼제어 시스템이 새로운 것은 전혀 아니다.
> RCS, CVS, Subversion 같은 도구는 이제 레거시 시스템(legacy system)으로 간주된다.
> 이들 과거 시스템은 최근에 등장한 도구 Git과 [Mercurial](http://swcarpentry.github.io/hg-novice/)보다
> 더 제한된 능력을 제공했다.
> 특히 최근에 등장한 도구는 *분산기능*을 제공한다.
> 저장소를 굳이 중앙 서버에 둘 필요가 없다는 의미다.
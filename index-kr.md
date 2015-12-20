---
layout: page
title: Git을 사용한 버젼 관리
---

Universal Missions 회사는 (Euphoric State University에서 분사한 항공 서비스 전문회사) 늑대인가(Wolfman)과 드라큘라(Dracula)를 고용해서 다음 행성 착륙선을 화성에 보낼 수 있는지 조사하려고 한다. 늑대인간과 드라큘라 모두 계획하는 작업을 동시에 수행할 수 있길 희망하지만, 과거에도 동일한 문제에 봉착한 경험이 있다. 순서대로 작업을 한다면, 다른 사람 작업이 끝날 때까지 한참을 기다려야 한다. 하지만, 본인 계획을 가지고 작업을 해서 전자 우편으로 주고 받고 하는 것은 분실되고, 덮어쓰고, 이중기록되는 문제가 있다.

한 동료가 작업관리로 [버젼 제어(version control)](reference.html#version-control)를 제안했다.
버젼 제어가 전자우편을 주고 받는 것보다 낫다:

*   버젼 제어에 커밋된 어떤 것도 분실되지 않는다. 모든 과거 파일 이력이 저장되기 때문에,
    항상 누가 무엇을 특정 시점에 작업한 것, 혹은 특정 결과를 생성하는데 무슨 프로그램 버젼을 사용했는지도 
    살펴보려 하면 시간여행해서 되돌아 보는 것도 가능하다.

*   누가 언제 언떤 변경을 했다는 기록을 보유하고 있어서, 추후 질문이 있다면 누구에게 물어봐야 되는지 알게 된다.
    그리고, 만약 필요하다면, 편집기에서 "실행 취소(undo)"와 매우 유사하게 이전 버젼으로 원복도 가능하다.

*   동일 프로젝트에 여러명이 협업할 때, 실수로 누군가의 변경사항을 간과하거나 덮어쓰곤 한다:
    버젼제어 시스템은 자동적으로 사용자에게 알람을 줘서 본인 작업과 다른 사람 작업사이에 충돌(conflict)이 있다는 것을 알 수 있다.

팀으로 작업하는 사람만 버젼제어로부터 혜택을 받는 것은 아니다: 
단독 연구자도 상당히 혜택을 받을 수 있다. 만약 추후에 해당 프로젝트로 되돌아 볼 필요가 있다면 (예를 들어, 기억이 희미해지는 1년 후에),
무엇이 언제, 왜 변경되었는지 기록을 보관하는 것이 모든 연구자에게 극도로 중요하다.

버젼관리 (Version Control)은 디저털 세상에서 연구실 수첩이다:
버젼관리는 전문가가 자신이 한것과 다른 사람과 협업한 것을 기록하고 관리하기 위해서 사용하는 것이다. 
모든 대형 소프트웨어 개발 프로젝트는 버젼제어에 의존하며, 
대부분의 프로그래머는 작은 일에도 사용한다. 
버젼제어가 단지 소프트웨어만 한정된 것이 아니다. 
책, 논문, 작은 데이터셋, 시간에 따라 변하고 공유될 필요가 있는 어떤 것이나 버젼제어 시스템에 저장될 수 있고 되여야 한다.

> ## 전제조건 {.prereq}
>
> 이번 학습에서 유닉스 쉘에서 Git을 사용한다.
> 쉘을 사용한 이전 경험 일부를 기대하지만, *강제적인 의무사항은 아니다.*

> ## 사전 준비 {.getready}
>
> 사전에 준비할 것은 없다: 출발 준비가 되었다!

## 학습주제
|   한국어(Korean)      |    영어(English)            |
|------------------------|---------------------------|
|1.  [자동화된 버젼제어](01-basics-kr.html)             | 1.  [Automated Version Control](01-basics.html)   |
|2.  [Git 구축 및 설정](02-setup-kr.html)                | 2.  [Setting Up Git](02-setup.html)                            |
|3.  [저장소 생성](03-create-kr.html)                      | 3.  [Creating a Repository](03-create.html)             |
|4.  [변경사항 추적](04-changes-kr.html)               | 4.  [Tracking Changes](04-changes.html)              |
|5.  [이력 탐색](05-history-kr.html)                       | 5.  [Exploring History](05-history.html)                     |
|6.  [관리에서 제외](06-ignore-kr.html)                   | 6.  [Ignoring Things](06-ignore.html)                        |
|7.  [GitHub 원격작업](07-github-kr.html)             | 7.  [Remotes in GitHub](07-github.html)                  |
|8.  [협업](08-collab-kr.html)                                 | 8.  [Collaborating](08-collab.html)                            |
|9.  [충돌](09-conflict-kr.html)                               | 9.  [Conflicts](09-conflict.html)                                 |
|10. [공개과학](10-open-kr.html)                           | 10. [Open Science](10-open.html)                          |
|11. [라이선싱](11-licensing-kr.html)                    | 11. [Licensing](11-licensing.html)                            |
|12. [호스팅](12-hosting-kr.html)                            | 12. [Hosting](12-hosting.html)                                 |
















 
## 추가 학습교재       

*   [참고문헌](reference.html)
*   [토론](discussion.html)
*   [강사 안내서](instructors.html)

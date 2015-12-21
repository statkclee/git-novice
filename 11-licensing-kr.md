---
layout: page
title: Git을 사용한 버젼 관리
subtitle: 라이선싱
minutes: 10
---
> ## 학습 목표 {.objectives}
>
> *   프로젝트 저장소에 라이선싱정보와 인용정보를 달아두는 것이 중요한지 설명한다.
> *   적절한 라이선스를 선정한다.
> *   라이선싱에 차이점과 사회적 기대를 설명한다.

소스코드, 원고, 다른 창의적 저작물을 갖는 저장소가 공개될 때,
저장소 기반 디렉토리에 `LICENSE` 혹은 `LICENSE.txt` 파일을 포함해서 콘텐츠가 어떤 라이선스로 이용가능한지를 명확히 기술해야된다.
이유는 소스코드가 창의적 저작물로서, 자동적으로 지적재산(따라서 저작권)보호에 대상에 부합되기 때문이다. 자유로이 이용가능한 것으로 보여지거나, 명시적으로 광고되는 코드는 그런 보호를 유예하지 *않는다*. 따라서, 라이선스 문장이 없는 코드를 (재)사용하는 누구나 스스로 위험에 처하게 된다. 왜냐하면 소프트웨어 코드 저자가 항상 일방향으로 재사용을 불법화할 수 있기 때문이다.



A license solves this problem by granting rights to others (the
licensees) that they would otherwise not have. What rights are being
granted under which conditions differs, often only slightly, from one
license to another. In contrast to proprietary licenses, the
[open licences](http://opensource.org/licenses/alphabetical) certified by
the [Open Source Initiative](http://opensource.org/) all grant at
least the following rights, referred to as the
[Open Source Definition](http://opensource.org/osd):

1. The source code is available, and may be used and redistributed
   without restrictions, including as part of aggregate distributions.
2. Modifications or other derived works are allowed, and can be
   redistributed as well.
3. The question of who receives these rights is not subject to
   discrimination, including not by fields of endeavor such as
   commercial versus academic.

How best to choose an appropriate license can seem daunting, given how
many possibilities there are. In practice, a few licenses are by far
the most popular, including the following:

* [GNU General Public License](http://opensource.org/licenses/GPL-3.0)
  (GPL),
* [MIT license](http://opensource.org/licenses/MIT),
* [BSD license](http://opensource.org/licenses/BSD-2-Clause),
* [Apache license, Version 2.0](http://opensource.org/licenses/Apache-2.0).

The GPL is different from most other open source licenses in that it
is
[infective](http://swcarpentry.github.io/git-novice/reference.html#infective):
anyone who distributes a modified version of the code, or anything
that includes GPL'ed code, must make *their* code freely available as
well.

The following article provides an excellent overview of licensing and
licensing options from the perspective of scientists who also write
code:

> Morin, A., Urban, J., and Sliz, P. “[A Quick Guide to Software
> Licensing for the Scientist-Programmer](http://dx.doi.org/10.1371/journal.pcbi.1002598)” PLoS Computational Biology
> 8(7) (2012): e1002598.

At the end of the day what matters is that there is a clear statement
as to what the license is, and that the license is one already vetted
and approved by [OSI](http://opensource.org). Also, the license is
best chosen from the get-go, even if for a repository that is not
public. Pushing off the decision only makes it more complicated later,
because each time a new collaborator starts contributing, they, too,
hold copyright and will thus need to be asked for approval once a
license is chosen.

If the content of a repository contains reseach products other than
software, such as data, and/or creative writing (manuals, technical
reports, manuscripts), most licenses designed for software are _not_
suitable.

* **Data:** In most jurisdictions most types of data (with possibly
  the exception of photos, medical images, etc) are considered facts
  of nature, and are hence not eligible for copyright
  protection. Therefore, using a license, which by definition asserts
  copyright, to signal social or scholarly expectations for
  attribution serves only to create a legally murky situation. It is
  much better to clarify the legal side with a public domain waiver
  such as
  [Creative Commons Zero (CC0)](https://creativecommons.org/publicdomain/zero/1.0/),
  and the social expectations side with express requests for how to
  use and cite the data. The [Dryad](http://datadryad.org) data
  repository in fact requires this.

* **Creative works:** Manuals, reports, manuscripts and other
  creative works are eligible for intellectual property protection and
  are hence automatically protected by copyright, just as software source
  code. [Creative Commons](http://creativecommons.org/) has prepared a
  [set of licenses](http://creativecommons.org/licenses/) using
  combinations of four basic restrictions:

    * Attribution: derived works must give the original author credit
      for their work.
    * No Derivatives: people may copy the work, but must pass it along
      unchanged.
    * Share Alike: derivative works must license their work under the
      same terms as the original.
    * Noncommercial: free use is allowed, but commercial use is not.

  Only the Attribution
  ([CC-BY](http://creativecommons.org/licenses/by/4.0/)) and
  Share-Alike
  ([CC-BY-SA](http://creativecommons.org/licenses/by-sa/4.0/))
  licenses are considered "[Open](http://opendefinition.org/)".

[Software Carpentry](http://software-carpentry.org/license.html)
uses CC-BY for its lessons and the MIT License for its code
in order to encourage the widest possible re-use.
Again,
the most important thing is for the `LICENSE` file in the root directory of your project
to state clearly what your license is.
You may also want to include a file called `CITATION` or `CITATION.txt`
that describes how to reference your project;
the one for Software Carpentry states:

~~~
To reference Software Carpentry in publications, please cite both of the following:

Greg Wilson: "Software Carpentry: Lessons Learned". arXiv:1307.5448, July 2013.

@online{wilson-software-carpentry-2013,
  author      = {Greg Wilson},
  title       = {Software Carpentry: Lessons Learned},
  version     = {1},
  date        = {2013-07-20},
  eprinttype  = {arxiv},
  eprint      = {1307.5448}
}
~~~

> ## Can I Use Open License? {.challenge}
>
> Find out whether you are allowed to apply an open license to your software.
> Can you do this unilaterally,
> or do you need permission from someone in your institution?
> If so, who?

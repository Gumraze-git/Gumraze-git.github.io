---
title: 버전 관리 시스템과 Git의 시작.
date: 2024-12-4-15:00:00
category: Git
layout: post
comments: true
image:
  path: assets/attachment/git/Git_Logo_2.png
  
tag: [Bootcamp, Woowa, Git, Commit, Convention]
description: Version Control System & The Stupid Content Tracker
pin: false
---

## **시작하면서...**
혼자서 공부하고, 혼자서 문제를 해결하는 것이 편안했던 나는 Git을 이용하는 것이 조금 불편했었다.
그런데, 개발을 공부하면서 Git을 통해 많은 것을 배우고 Git을 사용하는 일이 점점 많아졌다.
또한, 많은 과업들이 동료와 함께 완성해 나감의 미학을 배우게 되었다.

![about_git_0.png](/assets/attachment/git/about_git_0.png)
_왼쪽 순서대로 GitHub, Git, Linux Logo_

**그 와중에 갑자기 Git을 누가 만들었는지 궁금했다.**  
오늘은 **버전 관리 시스템과 Git**에 대해 알아본 내용을 공유하고자 한다.

- - -

## **버전 관리 시스템**
**버전 관리 시스템(VCS, Version Control System)**은 변경한 파일은 시간 순서대로 기록한 뒤, 특정 시점의 파일의 버전을 다시 꺼내올 수 있는 시스템이다.

VCS를 사용하면 각 파일을 이전 상태로 되돌릴 수 있고, 프로젝트를 통째로 이전 시점으로 되돌릴 수 있다.
또한, 누가 문제를 일으켰는지 추적할 수 있고, 누가 언제 만들어낸 이슈인지도 알 수 있다.
VCS를 사용하면 파일을 잃어버리거나 잘 못 고쳤을 때에도 쉽게 복구 할 수 있다.

### **로컬 버전 관리**
일반적으로 버전 관리 시스템에 대해 친숙하지 않은 사람들은 파일을 디렉토리에 복사하여 날짜, 시간 등을 기록하는 방법으로 버젼 관리를 한다.
이것을 **로컬 VCS**라고 한다.  

이러한 방법으로 버젼 관리를 하게 되면, 작업하던 디렉토리를 삭제하거나, 실수로 다른 파일을 수정 하는 등의 문제가 발생할 수 있다.

![about_git_1.png](/assets/attachment/git/about_git_1.png){: width="400" height="400"}
_로컬 VCS 버전 관리 예시_  

### **중앙 집중식 버전 관리(CVCS, Centralized Version Control System)**

**중앙 집중식 버전 관리 시스템**은 **다른 개발자와 함께 프로젝트를 진행할 경우를 위해 개발된 시스템**이다.
중앙에서 시스템 파일을 관리하는 서버가 별도로 존재하며, 사용자는 중앙 서버에서 파일을 **체크아웃(checkout)** 하여 사용 한다.  

CVCS 환경은 로컬 VCS과 비교하였을 때, 모두가 어떤 것을 작업하고 있는지 알 수 있는 장점이 있지만, 중앙 서버에 문제가 발생하면 모든 작업이 중단될 수 있는 치명적인 결함이 있다.

> 체크아웃(checkout): 버전 관리 시스템에서 특정 버전의 파일이나 디렉토리를 가져와 직업 디렉토리(로컬)에 복사하는 작업.
{: .prompt-tip }

![about_git_2.png](/assets/attachment/git/about_git_2.png){: width="400" height="400"}
_중앙 집중식 버전 관리 예시_ 

### **분산 버전 관리 시스템(Divided Version Control System)**
**Git의 시스템은 분산 버전 관리 시스템에 해당되며, 현재 개발자들에게 가장 표준화된 버전 관리 시스템이다.**
이 시스템은 단순히 파일의 마지막 버전을 체크아웃(checkout)하지 않고, DVCS는 저장소를 히스토리와 함께 복제하는 방법으로 작업 파일을 가져온다.  

만일 서버에 문제가 발생하는 경우, 위 작업 파일으로 작업을 시작할 수 있으므로 안전한 백업을 수행하면서 작업이 가능하다는 장점이 있다. 

![about_git_3.png](/assets/attachment/git/about_git_3.png){: width="400" height="400"}
_분산 버전 관리 시스템 예시_

- - -

## **Git의 시작**
### **리누스 토르발스(Linus Torvalds)**
**리누스 토르발스는 리눅스 커널의 창시자이자 분산 버전 제어 시스템인 Git을 개발한 소프트웨어 엔지니어이다.**
그는 리눅스 커널을 단지 새 PC 하드웨어가 어떻게 작동하는지 알아보기 위해 우발적으로 시작한 프로젝트라고 설명했다.
그렇게 리눅스 시스템을 임베디드 시스템에서 개인 PC와 슈퍼 컴퓨터 그리고 모바일 장치까지 사용하는 성공적인 시스템 그리고 프로젝트가 되었다.

![linus_torvalds.png](/assets/attachment/git/linus_torvalds.png){: width="400" height="400"}
_"Tech Talk: Linus Torvalds on git"에서의 리누스 토르발스(Linus Torvalds)_

리누스 토르발스는 리눅스를 개발하면서 저작권 라이센스를 아래와 같이 작성했다.
> **"you can distribute this in source form, but not for money."**  
> "당신은 이것을 소스 형태로 배포할 수 있지만, 상업적으로는 안됩니다."

나는 이것을 리누스 토르발스가 오픈소스(Open Source) 소프트웨어 대한 생각이 나타는 부분이라고 생각한다.
실제로도, 리누스 토르발스는 오픈소스가 소프트웨어를 개발하는 가장 올바른 방법이라고 믿었다.

### **리눅스의 버전 관리 시스템: Git**

![Git-Logo.svg](/assets/attachment/git/Git-Logo.svg)
_Git LOGO_

Git은 2005년 리누스 토르발스가 Linux 커널 개발 중 버전 관리를 위해 만든 시스템이다.

> 리누스 토르발스는 Git을 설계할 때, 내가 만일 예수라면 어떻게 Git을 만들 것인지 고민하면서 만들었다고 한다.

리누스 토르발스는 리눅스 커널 개발을 시작하고 오랜 기간 CVS(Concurrent Versions System) 및 SVN(Subversion) 등의 버전 관리 소프트웨어를 사용하지 않았다고 한다.
그 이유는 수많은 컨트리뷰터(contributer)가 개발하는 오픈소스인 리눅스 개발 환경에는 기존 버전 관리 소프트웨어가 구조 및 성능적으로 적합하지 않았다고 생각했기 때문이다.  

> **리누스 토르발스는 CVS를 매우 매우 매우 싫어했다고 한다.**  
> **심지어, CVS를 사용하는 사람은 이미 정신병원에 있어야 한다고 했다.**  
> **SVN 또한 매우 매우 매우 싫어하였는데, 그 이유는 SVN 개발 슬로건이 "잘 작동하는 CVS"이었기 때문이다.**  

따라서, 기존에는 유닉스 환경에서 개발된 **Tarball**과 **Patch** 기능을 이용하여 오랜 기간 소스 코드 관리를 수행했다.

간단히 설명하면, **Tarball**은 파일이나 디렉토리 묶음을 Tar(Tape Archive)라는 형식으로 엮은 파일이고,
**Patch**는 기존 파일의 변경 내용을 기록한 파일으로 두 파일 간의 차이를 차이점(diff)를 텍스트 형태로 저장하여,
변경 사항을 다른 파일에 적용 할 수 있도록 하는 기능이다.

그리고 **리누스 토르발스는 tarball과 petch를 아주 뛰어난 소스 제어 관리 툴이라고 생각했다.**  
하지만, 많은 리눅스 커널 개발자들은 다른 커널 개발자들이 이미 사용하고 있는 CVS 및 SVN 등의 버전 관리 시스템에 대한 갈망이 있었고,
리누스 토르발스는 2002년에 BitKeeper를 리눅스의 버전 관리 소프트웨어로 채택하게 되었다.

![Bitkeeper_logo.png](/assets/attachment/git/Bitkeeper_logo.png)
_BitKeeper Logo_

당시, 이러한 결정에 많은 사람들이 리누스 토르발스에게 많은 의문점을 가졌다.  
그 이유는 리누스 토르발스는 이미 오픈소스 소프트웨어 철학의 선구자이며,
그 철학에 감명받은 많은 리눅스 커널 개발자들은 이미 오픈소스 소프트웨어 광신도가 되어 있었기 때문이다.

하지만, 실제로 리누스 토르발스는 오픈소스 소프트웨어 광신자가 아니었다는 것이다.
리누스 토르발스는 오픈소스가 소프트웨어를 개발하는 유일한 올바른 방법이라고 생각함과 동시에,
작업에 가장 적합한 도구를 사용하는 것이 필요하며, 그것이 상용 소프트웨어일지라도 사용할 것이라고 했다.

> BitKeeper는 리눅스 커널 개발자 한정으로 소스를 오픈하였기에 리누스 토르발스는 BitKeeper를 사용했다.

그러나 결국, BitKeeper의 리버스 엔지니어링 사건으로 인해 오픈소스 라이선스는 철회되면서 리누스 토르발스는 Git이라는 대안을 개발하게 되었다.

> BitKeeper의 무료 라이선스가 철회된 계기는, 앤드류 트리젤(Andrew Tridgell)이 BitKeeper의 프로토콜을 리버스 엔지니어링하여 SourcePuller라는 도구를 만들었기 때문이다.  

### **Git의 개발 배경**
![about_git_4.png](/assets/attachment/git/about_git_4.png)
_Tech Talk: Linus Torvalds on git: Git 개발 배경_

Tech Talk 내용에 기반하여 Git의 개발 배경에 대해 스스로 해석해보자 한다.
> 주관적인 해석해본 내용이 틀릴 수도 있습니다.  
> 많은 지적, 조언 부탁드립니다. 😊

#### **I'm not an SCM(System Control Management) person**
리누스 토르발스의 전문 분야는 운영 체제 및 파일 시스템 개발이지 버전 관리 시스템의 legacy한 설계 방법과 사용법이 전문 분야가 아니었습니다.
따라서, **리누스 토르발스는 Git을 개발 할 때 버전 관리 시스템을 완벽히 이해하는 것보다 리눅스 커널 개발 프로젝트를 관리하는데 필요한 기능 및 그의 철학과 맟는 기능을 개발하고자 했다.**  

#### **Needed replacement for BitKeeper**
앞서 말했듯이 BitKeeper의 라이선스 종료로 인해 그의 대안을 찾고 있었는데, 기존에 있던 버전 관리 시스템은 성능이 너무 좋지 않거나 중앙 제어 시스템의 한계점을 분명히 가지고 있었다.  
따라서, **리누스 토르발스는 대안이 될 수 있는 시스템을 직접 개발하고자 했다.**

> 토르발스는 CVS를 사용하는 것을 좋아한다면, 정신병원에 있어야 한다고 했다.

#### **Some fundamental requirements**
리누스 토르발스는 버전 관리 시스템에 대해 몇 가지 기본적인 요구조건에 대해 말했다.  
그 중 3가지에 대해 이야기 해보고자 한다.  

- **시스템이 분산(distribute)되지 않으면 사용할 가치가 없다.**  
  당시, 대부분의 중앙 집중식 시스템은 작업을 필요로 할 때, 정상적으로 작동할 수 없다고 했다.
  그 예시로 인터넷이 연결되지 않은 상황등 여러 조건에서 사용이 불가하기 때문이다.
  또한, 모든 개발자들에게 커밋(commit)권한을 줄 수 없으므로 시스템이 분산되어 있어야하며,
  분산환경에서는 개발자가 자신의 저장소에 어떤 짓이든 해도 관계없어야 한다고 했다.

![about_git_5.png](/assets/attachment/git/about_git_5.png){: width="600" height="600"}
_분산환경에서의 개발자의 저장소가 가지는 자유도 [[출처]](https://joone.net/2022/10/02/47-git/)_

- **시스템의 성능이 나쁘면 사용할 가치가 없다.**
  리눅스 커널 프로젝트는 아주 큰 프로젝트이므로 코드 업데이트, 합병(merge), 브랜치(branch) 작업이 빠르게 끝나야 한다고 생각했다.
  이것은 1번과 같은 맥락으로 시스템이 중앙에서 처리하는 것보다 분산되어 있어야 작업 성능이 좋아진다.
 
![about_git_6.png](/assets/attachment/git/about_git_6.png){: width="500" height="500"}
_분산환경에서의 시스템 처리 성능 [[출처]](https://joone.net/2022/10/02/47-git/)_

- **SCM에 입력한 내용을 체크아웃했을 때 내용일 정확히 동일하다고 보장 할 수 없으면, 사용할 가치가 없다.**  
  토르발스는 대부분의 버전 관리 시스템에서 파일의 무결성을 확인하지 않는다는 것을 지적했다.
  CVS 및 SVC등의 버전 관리 시스템에서는 파일의 무결성을 체크아웃 이후 개발자가 파일의 무결성을 직접 확인해야한다는 단점이 있었다.

>오픈소스에 대한 리누스 토르발스의 개발 철학을 기반으로 모든 개발자들의 친구인 **GIT**이 탄생하게 되었다.
{: .prompt-info }

# **출처**
- [git.git readme](https://git.kernel.org/pub/scm/git/git.git/about/)
- [Wikipedia: Git](https://en.wikipedia.org/wiki/Git)
- [Wikipedia: Linus_Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds)
- [Wikipedia: History of Linux](https://en.wikipedia.org/wiki/History_of_Linux)
- [Wikipedia: Linus's law](https://en.wikipedia.org/wiki/Linus%27s_law)
- [Tech Talk: Linus Torvalds on git](https://youtu.be/4XpnKHJAok8?si=nxzCa4Jv0zVDdDNA)
- [A Git Origin Story](https://www.linuxjournal.com/content/git-origin-story)
- [30 Years Of Linux: An Interview With Linus Torvalds](https://www.tag1consulting.com/blog/interview-linus-torvalds-linux-and-git)
- [30 Years Of Linux: An Interview With Linus Torvalds(한국어 버전)](https://sjp38.github.io/ko/post/torvalds_interview_for_30th_anniversary_of_linux_kernel_part1/)
- [만화로 나누는 자유/오픈소스 소프트웨어 이야기/GIT](https://joone.net/2022/10/02/47-git/)

---
title: Git 커밋 메시지 규칙을 알아보자! (AngularJS)
date: 2024-12-22 15:07:00 +0900
layout: post
category: Git
comments: true
tag: [Git, AngualrJS, Commit, Convention, Woowa]
image:
  path: assets/attachment/git/Git_Logo_2.png
description: AngularJS Commit Convention
pin: false
---
- - -
## **시작하면서,,,**
작업한 내용을 Git에 스테이징 후, 커밋을 위해 커밋 메시지를 작성해야한다.
커밋 메시지를 처음에는 어차피 누군가 리뷰하지도 않는다는 생각에 대충 작성했었다.

그런데, 우아한 프리코스를 통해서 이제는 커밋 메시지를 작성하고 나의 코드 그리고 Git을 평가받게 되었는데,
지금까지 제대로 커밋 메시지를 작성한 경험이 없어 큰 벽을 느꼈다.

따라서, 우아한 프리코스의 교육으로 알게된 **AngularJS Git Commit Message Convention에 대해 정리**해보고,
간단히 다른 커밋 메시지 규칙들도 알아보고자 이 글을 적게 되었다.

> **필요한 내용만 찾고자 하는 분은 링크를 통해 해당 글로 이동하면 됩니다.**
- [Git Commit Convention의 종류](#git-commit-convention의-종류)  
  > Git Commit Convention의 종류를 정리하지만, AngularJS Commit Convention만 다루고자 한다.
- [AngularJS Commit Convention](#angularjs)
- [좋은 Git Commit 메시지 작성하는 방법](#좋은-git-commit-메시지를-작성하는-방법)

- - -
## **Git Commit Convention의 종류**
구글링을 통해 찾을 수 있는 커밋 컨벤션은 아래와 같다.
- [AngularJS Commit Message Convention](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)
- [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)
- [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)
- etc...

위 컨벤션을 포함한 대부분의 Git 커밋 컨벤션은 **AngularJS Commit Message Convention에 기반**하여 몇 가지 형식을 변경하여 사용되고 있었다.
따라서 기초가 되는 AngularJS Commit Message Convention에 대해 알아보고자 한다.

- - -
## **AngularJS??**
AngularJS는 구글의 엔지니어가 개발한 JavaScript를 이용한 오픈소스 프론트엔드 웹 개발 프레임워크이다.

> AngularJS에 대한 지원은 2022년 1월 부로 종료됨.  
> 현재는 Angular라는 이름으로 TypeScript를 이용한 웹 개발 프레임워크를 지원하고 있음.

AngularJS Git Commit Message Convention은 간단히 말해서 AngularJS를 개발할 때의 Git 커밋 메시지 작성 규칙이다.
- - -
## **AngularJS Git Commit Message Rule**
아래 내용은 [AngularJS Git Commit Message Rule](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit?tab=t.0#heading=h.7mqxm4jekyct)를 번역한 내용입니다.

> 원본 문서의 일부 생략하였고, 이해를 위해 번역한 내용의 일부 의역했습니다.  
> 틀린 내용이 있으면 댓글로 수정 부탁드리며, 정확한 내용은 [원본 문서](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit?tab=t.0#heading=h.7mqxm4jekyct)를 참고하시길 바랍니다.
 
### **개발 배경**
#### **중요하지 않은 커밋 식별**
개발을 하다보면 공백 추가 및 제거, 들여쓰기 수정, 오타 수정 등을 하게되는 경우가 있다. 
이러한 경우 로직의 변경이 없으므로 비교적 중요하지 않은 커밋으로 취급될 수 있다.
```text
예시)
Removing Empty lines
Adding indentation
```
위와 같은 커밋이 있는 경우에 변경사항을 찾고자 할 때 오랜 시간이 걸리게 된다.

#### **히스토리 탐색 시 불편**
개발자들은 코드 변경 및 수정 시 히스토리를 커밋 메시지에 작성한다.
또한, 맥락(context)를 추가하여 히스토리를 찾을 때 더욱 편리하게 하려고 한다.
```
예시)
Fix small typo in docs widget
Fix test for scenario.Application - should remove old iframe
Replaced double line break with single when text is fetched from Google
fixing broken links
fix comment stripping
Bit of refactoring
```
그런데 위와 같은 커밋 메시지에는 형식이나 규칙이 없어서 히스토리를 탐색하는데 어려움이 있다.

### **목표**
**중요하지 않은 커밋을 식별**하고 **히스토리 탐색을 편리**하게 하기 위해서 Git 커밋 컨벤션을 정하게 되었으며,
추가적으로 자동화를 위해 원본 문서에는 AngularJS Git Commit Convention의 목표를 아래와 같이 명시하고 있다.

- **스크립트를 통해 CHANGELOG.md를 자동으로 생성할 수 있도록 함.**
  - CHANGELOG.md의 구성
    - 새로운 기능(new features)
    - 버그 수정(bug fixes)
    - 주요 변경 사항(breaking changes)
- **중요하지 않은 commit 구분.**
  - 형식 변경 등과 같이 중요한 변경이 아닌 Commit을 git bisect로 무시 가능하게 함.
- **히스토리 탐색 시, 정보 제공.**

> 이번 게시글은 Git 커밋 메시지 작성하는 방법을 다루고자하여, 커밋 메시지 형식만 다루고자 한다.

### **AngularJS Git Commit Message 형식**
AngularJS Git Commit Message의 형식은 아래와 같이 작성되며, 3가지 섹션으로 구분되어 있음.
```text
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

1. **Message header(메시지 머리말)**
   1. Type(유형)
   2. Scope(범위)
   3. subject(제목)
2. **Message body(메시지 본문)**
3. **Footer(꼬리말**)

**전체 Commit Message의 지켜야할 규칙은 다음과 같다.**
- 커밋 메시지의 각 줄은 최대 100자를 넘지 않아야함.
  - GitHub 및 다양한 도구에서의 호환성 때문임.
    > 일반적으로 버전 관리 도구에서 표시할 수 있는 글자의 수가 100자 이내임.
- 각 섹션은 빈 줄로 구분되어야함.
  - 마찬가지로 버전 관리 도구에서의 호환성을 위해 빈 줄로 구분해야함.
    > Git 명령어는 커밋 메시지를 빈 줄으로 섹션을 구분하고 분석함.

#### **Message header**
- 헤더는 단일 줄로 작성하며, **변경 사항을 간결하게 설명**하는데 목적을 둠.
- **변경 사항 유형(Type) 작성 규칙**

  | Type     | 설명                |
|----------|-------------------|
  | feat     | 기능 추가(feature)    |
  | fix      | 버그 수정(bug fix)    |
  | docs     | 문서(documentation) |
  | style    | 스타일 수정(formatting, missing space etc) |
  | refactor | 로직 변경             |
  | test     | 테스트 추가            |
  | chore    | (코드 실행에 영향 없는) 프로젝트 관리 및 유지보수 |
 
- **변경사항 범위(Scope) 작성 규칙**
> 범위(Scope)는 커밋한 변경사항의 위치를 명시함.

  | Scope     | 설명                               |
|-----------|----------------------------------|
  | location  | 특정 위치 관련된 기능 추가 또는 변경사항          |
  | browser   | 브라우저와 관련된 버그 수정                  |
  | compile   | 코드 빌드 또는 컴파일 과정 관련 작업            |
  | rootScope | 애플리케이션 전역 상태 관리 관련 변경            |
  | ngHref    | AngularJS의 ngHref 디렉티브 관련 작업 변경  |
  | ngClick   | AngularJS의 ngClick 디렉티브 관련 작업 변경 |
  | ngView    | AngularJS의 ngView 디렉티브와 관련 작업 변경 |
  | etc       | ...                              |

- **변경사항 주제(Subject) 작성 규칙**
  - 변경사항에 대한 간단한 설명을 작성함.
  - 명령형 현재시제(Imperative present tense)로 작성.
  - 첫 글자를 대문자로 작성하지 않음.
    - ex) change(o)/ changes(x)/ changed(x)
  - 마침표를 붙이지 않음.

#### **Message body**
- 주제(subject)와 마찬가지로 명형형 현재 시제를 사용함.
- 변경에 대한 동기를 포함하고, 이전 동작과의 차이를 설명함.

#### **Footer**
- 주요 변경사항은 푸터에 "BREAKING CHANGE:"로 시작하는 블록으로 명시함.
> 일반적으로 "BREAKING CHANGE:"는 주요 변경사항이 호환성의 문제를 발생시킬 수 있는 경우의 상세한 내용을 작성함. 
{: .prompt-info }
- 변경사항 작성 후, 변경 사항에 대한 설명 및 마이그레이션 가이드가 작성되어야함.
- Issue 참조
  - 해결된 버그는 푸터에 별도의 줄로 작성되며, Closes 키워드로 시작해야함.
  ```text
  Closes #123, #234, #456
  ```

#### **Revert**
이전 커밋을 수정하고자 할 경우, 아래 가이드를 따라야한다.
- 헤더는 "revert:"로 시작해야함.
- 본문에는 아래와 같은 내용이 포함되어야함.
  ```text
  This reverts commit <hash>.
  ```
> \<hash\>는 되돌리는 커밋의 SHA(Secure Hash Algorithm)값을 의미함.

### **작성 예시**
작성 예시는 용어 및 기능의 구체적인 변경보다 작성하는 방법을 참고해주면 됩니다. 

#### **예시 1**
```text
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```
- Type: feat
  - 새로운 기능이 추가됨.
- Scope: $browser
  - 변경 사항이 $browser 모듈에 영향을 미침.
- Subject: onURLChange event가 추가됨.
- 본문
  - popstate 이벤트 지원.
  - hashchange 이벤트 지원.
  - 브라우저가 popstate와 hashchange 이벤트를 모두 지원하지 않는 경우, 풀링(polling) 방식으로 URL 변경사항을 확인함.

#### **예시 2**

```text
fix($compile): couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
Breaks foo.bar api, foo.baz should be used instead
```
- Type: fix
  - 버그 수정임을 나타냄.
- Scope: $compile
  - 수정 사항이 $compile 모듈과 관련 있음.
- Subject: IE9에 대한 몇 가지 유닛 테스트의 수정 작업임을 나타냄.
- 본문
  - 문제 설명
    - 구버전 IE(Internet Explorer)에서는 HTML이 대문자로 직렬화(serialization)됨.
    - IE9에서는 HTML 직렬화 시 대소문자를 구분하지 않음.
  - 해결 방안
    - 대소문자를 구분하지 않는 비교를 하는 것이 해결책일 수 있으나,
    - Jasemin(테스트 프레임워크)에서는 예외 처리 검사 시, 정규식을 지원하지 않아서 이를 구현하기 어려움.
- Footer
  - Closes#392
    - 이 커밋은 GitHub 이슈 번호 #392와 관련이 있으며, 이 커밋으로 해당 이슈가 해결되었음을 의미함.
    - > GitHub는 이슈를 "Closes#n"의 양식으로 작성하면 이를 자동으로 닫는 작업이 이루어짐. 
  - foo.bar API가 제거되고 foo.baz API 사용을 권장함.
    - > 이는 기존 코드가 수정되지 않으면 동작하지 않을 수 있음을 나타냄.

#### **예시 3**   
```text
style($location): add couple of missing semi colons
```
- Type: style
  - 커밋의 목적이 코드의 형식이나 구조를 다듬는 스타일 개선임.
- Scope: $location
  - 변경 사항이 $location 모듈과 관련 있음.
- Subject: 누락된 세미콜론을 몇 개 추가함.

#### **예시 4**
```text
docs(guide): updated fixed docs from Google Docs

Couple of typos fixed:
- indentation
- batchLogbatchLog -> batchLog
- start periodic checking
- missing brace
```
- Type: docs
  - 커밋의 목적이 문서 수정임.
- Scope: 수정된 문서가 가이드와 관련 있음.
- Subject: Google Docs를 기반으로 수정된 문서 내용을 업데이트 함.
- 본문: 몇 가지 오탈자(typo)를 수정함.

- - -
## **좋은 Git Commit 메시지를 작성하는 방법**
### **Git Commit 메시지의 목적?**
많은 사람들은 커밋 메시지를 "**내가 무엇을 했는지**"를 기록하는 것으로 생각한다.
그러나 **Git은 분산 버전 관리 시스템**으로 다양한 소스에서 변경 사항을 가져오고 개발 할 수 있다.
그렇기 때문에 커밋 메시지는 "**내가 한 것**"이 아니라 "**이 커밋이 적용되면 어떤 변경 사항이 가져와 지는지**"를 설명해야한다.
변경 사항에 대한 동기를 설명하고, 이전 동작과의 차이를 명시함으로 커밋을 가져올 지, 가져오지 않을 지 결정 할 수 있도록 작성되어야한다.
> 본문은 무엇을? 왜? 변경하였는지에 초점을 맞추어 작성해야하며,  
> 필요한 내용을 짧고 간결하게 작성하는 연습이 필요하다.

**위 목적이 곧, Git Commit 메시지를 잘 작성하기 위한 방법이다.**

### **좋은 commit 메시지를 위한 영어.**
위 AngularJS Git Commit Message를 포함한 커밋 메시지 작성 규칙들은 기본적으로 영어로 작성된다.
영어가 모국어이면 커밋 메시지를 작성하는데 어려움이 적겠지만,,,

우선 영어가 모국어가 아니니, 영어로 작성하는 팁을 찾아보았고 다음 [좋은 git commit 메시지를 위한 영어 사전](https://blog.ull.im/engineering/2019/03/10/logs-on-git.html)에서 내용을 발췌하여 정리하였다.
굳이 영어로 작성해도 되는 경우가 아니면 개인적으로는 한국어로 작성하는게 맞다고 생각한다.

> 한국어로 작성하게 되면, 커밋 메시지 작성 규칙을 더욱 유연하게 적용하되 가독성을 고려하여 일관성 있게 작성하는게 중요할 것 같다.

#### **영문 커밋 메시지 작성 팁**
- 동명사보다 의미를 잘 표현할 수 있는 명사를 찾아서 사용해는 것이 가독성에 좋음.
  > ChatGPT에게 물어보자,,,
- 관사는 사용하지 않음.
- 부정문(Don't)을 사용함.
  - 부정 명령문을 사용하자.

#### **Git 커밋을 위한 영어사전**
- - -
##### **Fix**
> 올바르지 않은 동작을 고친 경우 사용함.

| **Pattern**                 | **Description**   |
|-----------------------------|-------------------|
| Fix A                       | A를 수정했음.          |
| Fix A in B                  | B의 A를 수정했음.       |
| Fix A that(which) B         | B 내용의 A를 수정함.     |
| Fix A to (be) B             | B를 위해 A를 수정함.     |
| Fix A so that B             | A를 수정해서 B가 되었습니다. |
| Fix A where B               | B처럼 발생하는 A를 수정함.  |

- - -

##### **Add**
> 코드나 테스트, 예제, 문서 등의 추가가 있을 때 사용함.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Add A                       | A를 추가함.         |
| Add A for B                 | B를 위해 A를 추가함.   |
| Add A to B                  | B에 A를 추가함.      |

- - -

##### **Remove**
> 코드 삭제 시 사용하며, Clean/Eliminate를 사용하기도 함.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Remove A                    | A를 삭제함.         |
| Remove A from B             | B에서 A를 삭제함.     |

- - -

##### **Use**
> 특별히 무언가를 사용하여 구현하는 경우에 사용함.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Use A                       | A를 사용함.         |
| Use A for B                 | B에 A를 사용함.      |
| Use A to B                  | B가 되도록 A를 사용함.  |
| Use A in B                  | B에서 A를 사용함.     |
| Use A instead of B          | B 대신 A를 사용함.    |

- - -

##### **Refactor**
> 코드 (전면) 수정이 있는 경우 사용함.

| **Pattern**                 | **Description**    |
|-----------------------------|--------------------|
| Refactor A                  | A를 수정함.            |

- - -

##### **Simplify**
> 복잡한 코드를 단순화 할 때 사용함. Refactor보다 약한 수정의 경우 사용하는 표현.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Simplify A                  | A를 단순화함.        |

- - -

##### **Update**
> 개정이나 버전 업데이트가 있을 때 사용함.

| **Pattern**                 | **Description**  |
|-----------------------------|------------------|
| Update A to B               | A를 B로 업데이트함.     |
| Update A to B               | A를 B하기 위해 업데이트함. |

- - -

##### **Improve**
> 호환성, 테스트 커버리지, 성능, 접근성 등의 향상이 있는 경우 사용함.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Improve A                   | A를 향상함.         |

- - -

##### **Make**
> 기존 동작의 변경을 명시함. 새로운 구현의 경우 Make 대신 Add 사용.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Make A B                    | A를 B하게 만듬.      |

- - -

##### **Implement**
> 주목할 만한 구현체(implementation)를 완성 시 사용.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Implement A                 | A를 구현함.         |
| Implement A to B            | B를 위해 A를 구현함.   |

- - -

##### **Rename**
> 이름 변경이 있을 때 사용.

| **Pattern**                 | **Description** |
|-----------------------------|-----------------|
| Rename A to B               | 이름 A를 B로 변경함.   |

- - -
## **마치면서,,,**
커밋 메시지 작성 방법에 대해 정리하고 알아보았다.
나중 참고를 위해 가능한 자세히 적어보려고 했는데, 내용을 적절히 요약 정리하면서 내용이 주제를 벗어나지 않도록 작성하는데 어려웠다.

스스로 정리하면서 커밋 메시지에 대한 많은 이해를 했고 커밋 메시지를 작성하는데 도움도 많이 되었다.
AngularJS Commmit Message Convention의 목표인 자동화까지는 다루지 못했는데, 추후 간단하게 다뤄보고자 한다.

마지막으로 우아한 프리코스 등 프로젝트를 수행하면서 느낀점은 커밋 메시지를 한 줄로 작성하기 위해 커밋 단위를 잘 분리하는 것도 정말 쉽지 않은 일이다.
그래도 기능 단위로 잘 분리하면 조금 도움이 된다.

## **3줄 요약.**
- 커밋 메시지는 버전 관리를 하기 위해 남기는 글이다.
- 내가 이번 주에 무엇을 한 것이 중요한게 아니라, 이 변경이 무엇인지 설명해라.
- 커밋 메시지는 짧고 간결하게!

## 출처
- [AngularJS](https://angularjs.org/)
- [What is Angular](https://www.angular.kr/guide/what-is-angular)
- [좋은 git 커밋 메시지를 작성하기 위한 7가지 약속(번역 및 정리)](https://meetup.nhncloud.com/posts/106)
- [How to Write a Git Commit Message](https://cbea.ms/git-commit/)
- [좋은 git commit 메시지를 위한 영어 사전](https://blog.ull.im/engineering/2019/03/10/logs-on-git.html)
- [Conventional Commit Messages](https://gist.github.com/qoomon/5dfcdf8eec66a051ecd85625518cfd13)
- [AngularJS Git Commit Convention 문서](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit?tab=t.0#heading=h.7mqxm4jekyct)
- [Google: 커밋 메시지 가이드](https://developers.google.com/blockly/guides/contribute/get-started/commits?hl=ko)
- [Git: Committing changes to your project](https://docs.github.com/en/pull-requests/committing-changes-to-your-project)
- [Writing Git commit messages](https://365git.tumblr.com/post/3308646748/writing-git-commit-messages)
- [A Note About Git Commit Messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
- Green, B., & Seshadri, S. (2013). AngularJS. " O'Reilly Media, Inc.".

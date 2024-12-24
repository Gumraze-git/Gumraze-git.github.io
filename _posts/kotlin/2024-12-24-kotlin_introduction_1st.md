---
title: "[Introduction to Kotlin] Kotlin 개발 배경 및 기본 구문(syntax)"
date: 2024-12-24 15:00:00 +0900
layout: post
category: Kotlin
comments: true
tag: [Kotlin, Java, JetBrain]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Introduction for Basic Kotlin
pin: false
---
- - -
## **시작하면서,,,**
모바일 개발자를 꿈꾸게 되면서 안드로이드냐, IOS냐 선택사항이 있었다.
그리고 추가적으로 크로스 플랫폼을 지원하는 플러터(Flutter)등의 언어냐, 스위프트(Swift) 등의 네이티브 언어냐에 대한 선택사항이 있었다.

**인생은 선택과 집중이다.**
![kotlin_homepage.png](/assets/attachment/kotlin_study/kotlin_homepage.png)
_Kotlin Homepage_

**나는 안드로이드 개발을 하는 코틀린(Kotlin)을 선택하였다.**
> 청소년기부터 지금까지 IOS를 사용했던 나는 코틀린을 선택하게 된 이유는 추후 모바일 개발자 로드맵을 알아보면서 자세히 설명해보고자 한다.

Python을 공부한 경험으로 프로그래밍 언어를 공부하는 방법 중 최고는 그냥 아무거나 구현해보는 것이라고 생각한다.  
그러나, 굳이 잘 만들어진 강의 자료가 있는데 맨땅에 헤딩할 필요는 없다고 생각한다.

코틀린 문서에 [Basic Syntax](https://kotlinlang.org/docs/basic-syntax.html)에 JetBrain의 Acadamy에서 지원하는 교육 홈페이지가 있다.
코틀린은 JetBrain에서 개발한 언어이다. 따라서, 위 교육 홈페이지에서 공부하면 좋을 것 같다고 생각하여 HyperSkill을 통해 공부한 내용을 공유하고다 한다.

> 본 게시글은 초보자를 위해 작성된 교육자료를 번역 및 의역한 내용이다.

- - -
## **Kotlin?** 
> HyperSkill을 통해 제작한 [Learn Kotlin/Introduction to Kotlin](https://hyperskill.org/study-plan)를 기반으로 작성됨.
> {: .prompt-info}


![kotlin_logo_2.png](/assets/attachment/kotlin_study/kotlin_logo_2.png)
### **Kotlin의 간략한 역사**

2011년 7월 JetBrain은 새로운 Java 플랫폼을 위한 Kotlin Project를 공개했다.
> Kotlin이라는 이름은 러시아 상트페테르부르크 근처의 Kotlin 섬에서 가져왔다.
![kotlin_island.png](/assets/attachment/kotlin_study/kotlin_island.png){: width="400" height="400" }
_Kotlin Island_

Java에는 아래와 같은 한계점 및 문제점이 있었다.
1. Null 안전성 문제
2. 보일러플레이트(Boilerplate) 코드
  > Java는 Getter/Setter 메서드, 데이터 클래스 등에서 비교적 긴 코드가 필요하다.  
  > 나는 Java를 해본적이 없어서 사실 잘 모른다,,,
3. 함수형 프로그래밍 지원 부족
4. etc..

따라서 Kotlin project의 목표는 현재 Java가 사용되는 모든 맥락에서 Java에 대한 더 안전하고 간결한 대안을 제공하는 것이었다.
1. 더 안전하고(Null 안전성, 컴파일러 오류 감소)
2. 더 간결하며(보일러플레이트 코드 제거, 직관적인 문법)
3. 더 생산적인 언어 제공(함수형 프로그래밍 지원 등)
4. etc

또한, Kotlin은 아래와 같은 차이점을 강조하고 있다.
- Kotlin의 기본 구문은 Java와 비슷하지만, 차이점이 있다.
  - 개발자가 상속을 사용하지 않고도 클래스의 기능을 확장할 수 있는 기능 등의 기능 차이가 있다.
  - Kotlin은 유형 추론(type inference)를 제공하여 컴파일러가 컨텍스트에 따라 변수의 유형을 결정할 수 있게 함.
    > 유형 추론을 이용하여 코딩을 간소화하고 오류를 줄일 수 있음.

Kotlin project의 공개 후, 많은 개발자 커뮤니티에서 Kotlin을 사용하는 것에 대해 관심이 많았다고 한다.
그 중 **안드로이드가 Kotlin에 대해 많은 관심을 가졌다.**
**안드로이드는 Java를 기반으로 개발**되었는데, Java의 한계를 극복하는데 Kotlin이 많은 도움이 될 것이라고 생각했다.
이후, Google I/O 2017 컨퍼런스에서 **Google은 Android에서 Kotlin에 대한 최고 지원(first-class support)을 하겠다고 발표**하면서,
안드로이드는 Kotlin을 기반으로 개발되고 있다. 그리고 Java를 사용하는 많은 플랫폼에서 사용되는 범용 언어가 되었다.
> 안드로이드의 최고 대변인(chief advocate) Chet Haase는 "We understand that not everybody is on Kotlin right now, but we believe that you should get there"라고 말함.

### **Kotlin을 위한 애플리케이션 플랫폼: JVM, Android, JS, Native**
- Kotlin은 JVM(Java Virtual Machine), Android, JavaScript, Native 등 다양한 애플리케이션 플랫폼에서 사용할 수 있다.
  - Java에 익숙한 개발자는 Android 기기에서 Kotlin을 사용하는 방법을 쉽게 배울 수 있음.
  - **Multiplatform**
    - **Kotlin Multiplatform**을 사용하면 애플리케이션 논리를 구현하기 위해 Android와 IOS 프로젝트 간의 코드를 공유하는 크로스 플랫폼 모바일 애플리케이션을 빌드 할 수 있음.
  - Kotlin은 실용적인 언어로 설계되어, 연구 목적보다 실제 문제를 해결하는 것을 목적으로 한다.
  - **Kotlin은 여러 프로그래밍 패러다임을 지원한다.**
    - 명령형 프로그래밍(imperative programming), **객체 지향 프로그래밍(object-oriented programming)**, 제네릭 프로그래밍(generic programming), 함수형 프로그래밍(functional programming) 등을 지원함. 
  - Kotlin은 도구 친화적인 언어로, InteliJ IDEA, Eclipse, Android Studio 등의 개발 도구와 호환된다.

- - -
## **Basic Literals: Numbers(숫자), Strings(문자열) and Characters(문자)**
> Literals: 모든 프로그램은 본질적으로 숫자, 문자열 및 기타 문자에 관한 연산을 수행함. 이러한 것들을 "literals"라고 함.
> {: .prompt-info}

### **Integer numbers**
현실 세계에서는 정수를 이용해서 사물을 세며, Kotlin에서는 0, 1, 2, 10, 11, 100 등으로 정수를 사용할 수 있다.
> **TIP**: 숫자가 많이 포함되어 있는 정수는 밑줄(`_`)을 이용하여 가독성을 높일 수 있는 기능도 제공한다.  
> Ex) 1000000 = 1_000_000 = 1___000___000  
> 숫자의 시작이나 끝에는 밑줄을 사용할 수 없다.  
> Ex) _1000000(x), _100_000_000_(x) 
{: .prompt-tip}

### **Characters(문자) & String(문자열)**
Java와 마찬가지로 Kotlin에서도 단일 문자(Characters)와 문자열(String)을 구분하여 사용한다.

#### **Characters(문자)**
- 단일 문자를 작성하려면 작은 따옴표로 기호를 감싸야한다.
  - Ex) 'A', 'B', 'C', etc
- 숫자를 나타내는 경우(9)와 단일 문자(characters)를 나타내는 경우('9')를 혼동하지 않도록 조심해야한다.
- 문자는 단일 기호를 나타내므로 2개 이상의 숫자나 문자를 포함할 수 없음.
  - Ex) 'A'(o)/ 'AB'(x) 

#### **String(문자열)**
- 문자열은 광고 문구, 웹 페이지 주소 등의 텍스트 정보를 나타낸다.
  - 문자열: 개별 문자들의 연속된 시퀀스
- 문자열을 작성할 때는 작은 따옴표('') 대신 큰 따옴표("")로 문자열을 감싸야한다.
  - Ex) "Kotlin", "I want to learn Kotlin", etc
- 문자열은 또한 단 하나의 문자만 포함할 수도 있다.
  - Ex) "A"≠'A'
  > 프로그래밍 효율성(메모리)가 중요하다면,  
  > 단일 문자 사용 시 작은 따옴표를 사용하고,  
  > 문자열 사용 시 큰 따옴표를 사용해야한다.  
  > 문자는 일반적으로 문자열보다 메모리를 적게 사용하기 때문임.  

## **Writing first program with Kotlin**
### **Basic terminology(기본 용어)**
1. **프로그램(Program)**
   - 프로그램은 "명령문(statement)"라고 불리는 일련의 지시사항으로 이루어져 있으며, 순차적으로 실행된다.
   - 가장 일반적이고 간단한 흐름은 명령문이 작성된 순서대로, 즉 위에서 아래로 하나씩 실행되는 순차적 흐름임.
2. **명령문(Statement, Programming Statement)**: 프로그램에서 실행할 단일 명령.
3. **표현식(Expression)**: 단일 값을 생성하는 코드 조각
   - Ex) 2 * 2
4. **블록(Block)**: 중괄호({...})로 묶여져 있는 명령문의 그룹이다. 프로그램은 여러 블록으로 구성되어 있다.
5. **키워드(Keyword)**: 프로그래밍 언어에서 특별한 의미를 가진 단어이다.
   - 키워드는 변경할 수 없다.
   - Ex) fun, main
6. **식별자(Identifier)**: 프로그래머가 무언가 식별하기 위해 작성하는 이름이다.
   - Ex) main
7. **주석(Comment)**: 프로그램 실행 시 무시되는 텍스트로, 코드의 일부를 설명하는데 사용된다.
8. **공백(Whitespace)**: 빈 공간, 탭 또는 줄 바꿈을 의미한다.

### **The Hello World program under a microscope**
#### **Hello World Program**
```kotlin
fun main() {
  println("Hello, World!")
}
```

#### **Entry Point(진입점)**
```kotlin
fun main() {
  // ...
}
```
- `fun` 키워드는 함수를 정의하며, 함수는 실행할 코드 조각을 포함한다.
- 이 함수는 특별한 이름(`main`)을 가지고 있으며, 함수는 중괄호로 둘러싸인 본문(body)를 가지고 있다.

> Note: 이 함수의 이름은 반드시 `main`이어야 한다.  
> `Main`, `MAIN` 등의 유사한 이름으로 작성하면 프로그램이 실행되지 않는다.
> {: .prompt-info }

#### **"Hello, World!" 출력하기**
```kotlin
println("Hello, World!")
```
- 이 함수의 본문은 프로그램이 수행할 작업을 정의하는 **프로그래밍 명령문(programming statement)** 으로 구성된다.
- "Hello, World!"는 문자열 리터럴(string literal)으로, 키워드나 이름이 아닌 단순히 출력할 텍스트이다.

> `println("...")`은 문자열을 화면에 출력하며, 출력 후 자동으로 줄바꿈이 되는 함수이다.    
> 일반적으로 Kotlin에서는 `println("...")`을 이용하여 출력문을 출력한다.
> {: .prompt-info }

#### **여러 명령문으로 구성된 프로그램**
- 일반적으로 프로그램은 여러 **명령문(statement)**으로 구성된다.
- 각 명령문은 새로운 줄에 작성하는 것이 원칙이다.
- Ex) Programs with multiple statements
  ```kotlin
  fun main() {
    println("Hello")
    println("World!")
  }
  ```
  아래는 위 코드를 실행한 결과이다.
  ```text
  Hello
  World
  ```
  

## **용어 정리**
- 컴파일러(Compiler): 프로그래밍 언어로 작성된 소스 코드를 기계어 또는 다른 형태의 코드 등으로 번역하는 프로그램
  - 즉, 사람이 작성한 프로그래밍 언어를 컴퓨터가 이해할 수 있는 언어로 번역하는 역할을 하는 것.
- 컨텍스트(Context): "문맥"으로, 특정 상황에서의 의미가 무엇인지를 설명함.
  - 프로그래밍 언어에서의 컨텍스트는 특정 코드가 어떤 환경에서 실행되는지 나타내는 문맥을 설명함.

## **3줄 요약**
- 코틀린 개발 배경을 알아보았다.
- 프로그래밍 언어를 한번이라도 경험해본 개발자에게는 쉬운 내용이다.
- 코틀린 syntax가 궁금하면 이 글에서 찾아보자.


## **출처**
- [Kotlin](https://kotlinlang.org/)
- [Introduction to Kotlin](https://hyperskill.org/courses/69-introduction-to-kotlin)
- [Kotlin으로 Android 앱 개발](https://developer.android.com/kotlin?hl=ko)
- [Kotlin Docs](https://kotlinlang.org/docs/home.html)
- [Learn Kotlin by Example](https://play.kotlinlang.org/byExample/overview?_gl=1*6rj97s*_gcl_au*MTYwMTUxMzIwNy4xNzM0NDE2OTg4*_ga*MTYxODcxOTU0MC4xNzMwODgxOTA5*_ga_9J976DJZ68*MTczNDQxNjk3OC40LjEuMTczNDQxOTQyNi42MC4wLjA.)
- [TIOBE Index: Programming language rank](https://www.tiobe.com/tiobe-index/)

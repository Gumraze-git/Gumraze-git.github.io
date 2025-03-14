---
title: "[Introduction to Kotlin] 프로그램 오류 및 예외 처리하기"
date: 2025-03-14 10:00:00 +0900
layout: post
category: [Kotlin]
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Short summary of the post.
pin: false
---
- - -

## **프로그램의 오류**

프로그램을 작성하다 보면, 컴파일 또는 실행하는 과정에서 다양한 오류가 발생 할 수 있다.  
일반적으로 이러한 **오류는 크게 두 가지 그룹으로 나눌 수 있다.**

1. **컴파일 타임 오류(compile-time errors)**
2. **런타임 오류(run-time errors)**

### **컴파일 타임 오류**

컴파일이란 우리가 작성하는 코드를 컴퓨터가 이해할 수 있는 기계어로 번역(변환)하는 작업을 의미한다.  
즉, 컴파일 타임 오류는 우리가 작성한 코드 중 어떠한 문제로 인해 기계어로 번역이 불가능 하다는 것이다.

예를 들면 다음과 같은 경우가 있다.

- **문법 오류(syntax errors)**: 잘못된 키워드 사용, 오타, 누락 등
- **잘못된 패키지 이름 호출(incorrect imported package name)**
- **존재하지 않는 메서드 호출(non-existing method invocation)**

다음은 컴파일 타임 오류의 예시이다.

```kotlin
fun main(args: Aray<String>) {
    printn("Hello!")
}
```
이 프로그램에는 **2 가지 오류**가 있다.

```kotlin
fun main(args: Aray<String>) {  // 1. Array 클래스 이름에 오타 발생.
    printn("Hello!")            // 2. println() 함수 이름에 오타 발생.
}
```
> 대부분 컴파일 타임의 오류는 오타인 경우가 많다.

이러한 오류들을 피하기 위해서는 정적 코드 분석 기능(static code analyzer)이 있는 IDE(Integrated Development Environment)를 사용하는 것이 좋다.
또한, 경험이 쌓이면 컴파일 타임 오류 없이 코드 작성이 가능해진다.

> 정적 코드 분석?  
> 코드를 실행하지 않고 소스 코드만을 분석하여 오류 및 코드 스타일 위반 등을 찾아내는 분석 방법이다.

> IDE는 컴파일 이전 오류를 식별할 수 있도록 도와주며, 복잡한 오류나 코드의 취약한 부분을 강조한다.  
> 심지어 코드의 개선 방법도 알려준다.

### **런타임 오류**
런타임 오류 즉, 버그(bug)는 프로그램이 실행되는 동안 발생하는 오류를 의미하며, 프로그램이 예상과 다르게 동작하거나 실행이 중단될 수 있다.

**런타임 오류는 크게 2 가지 유형으로 나뉜다.**

1. **논리 오류(logic errors)**: 코드의 논리가 올바르지 못하여 프로그램이 잘못된 결과를 출력하는 경우.
2. **예외 처리 되지 않은 오류(unhandled exceptions)**: 0으로 나누기, 찾을 수 없는 접근, 예기치 않은 입력 값 등의 의해 발생하는 오류.

**런타임 오류를 방지하는 것은 컴파일 오류를 방지하는 것보다 어렵다.**  
> 프로그램이 컴파일에 성공하더라도 버그가 없다는 보장은 없다.  

**런타임 오류를 방지하기 위해서는 다음과 같은 방법을 권장**한다.
- **디버깅(debugging)**: 프로그램을 실행하면서 오류를 추적하고 수정하는 과정.
- **자동화된 테스트 작성(automatic tests)**: 프로그램이 예상한 대로 동작하는지 확인하기 위해 테스트 코드 작성.
- **코드 리뷰(code review) 수행**: 개발 과정에서 한 명 이상의 개발자가 소스 코드를 직접 검토하는 과정.

- - -
## **예외**

예외(exception)는 예상하지 못한, 비 정상적인 이벤트의 발생으로 다양한 상황에서 발생한다.

아래 프로그램을 살펴보자.

```kotlin
fun readNextInt(): Int {    // 입력을 읽고 이를 숫자로 변환한 값을 반환한다.
    return readln().toInt()
}

fun runIncrementer() {      // readNextInt()의 반환 값에 1을 더한 뒤 반환한다.
    val increment = 1 + readNextInt()
    println(increment)
}

fun main() {                // runIncrementer()를 실행한다.
    runIncrementer()
}
```
위 프로그램에서 만약 사용자가 `twelve`을 입력하게 되면 어떤 일이 발생할까?

```text
> twelve
```

```text
Exception in thread "main" java.lang.NumberFormatException: For input string: "twelve"
	  at java.base/java.lang.NumberFormatException.forInputString(NumberFormatException.java:67)
	  at java.base/java.lang.Integer.parseInt(Integer.java:661)
	  at java.base/java.lang.Integer.parseInt(Integer.java:777)
	  at org.example.MainKt.readNextInt(Main.kt:4)
	  at org.example.MainKt.runIncrementer(Main.kt:8)
	  at org.example.MainKt.main(Main.kt:13)
	  at org.example.MainKt.main(Main.kt)
```

예외 발생 메시지를 읽어보면,
1. `main` 스레드(thread)에서 입력 문자열 `twelve`에서 예외 유형 `NumberFormatException`이 발생하였고,
2. 사용자 코드 4 번째 줄의 (`readNextInt(Main.kt:4)`)에서 오류가 발생하였으며,
3. 연쇄적으로 8 번째, 13 번째 줄에서 함수를 호출하면서 오류가 발생했다.

어떤 코드의 컴파일 타임, 링크 타임 오류 등은 프로그램이 실행되기 전에 발견될 수 있으나,  
**예외는 프로그램 실행 중(runtime)에 발생하는 오류이다.**

일반적으로 예외가 발생하는 이유는 다음과 같다.
- 잘못된 입력값(오타).
- 잘못된 연산 수행(ex, 0으로 나누기).
- 파일이나 네트워크에서 데이터를 찾을 수 없는 경우.
- 메모리 초과 등의 시스템 오류.

이러한 오류들은 예기치 않은 동작을 의미하며, 입력을 검증하거나 처리방식을 살펴보아야 한다.

- - -
## **예외의 계층 구조**
예외는 피할 수 없는 문제이다.  
그렇기 때문에 예외를 처리하기 위해 예외의 계층과 그 유형을 잘 알고 예외 발생 시 현명하게 처리하는 것이 중요하다.

**Kotlin의 여러 가지 예외 유형은 서로 연관되어 있으며, 특정 계층 구조를 형성**한다.

### **서브타입과 슈퍼타입**
Kotlin의 모든 타입들은 **서브타입(subtype)-슈퍼타입(supertype)관계**로 구성된 계층 구조를 이룬다.

간단하게, 커피와 차는 모두 음료라는 공통된 개념에 속한다.  
Kotlin에서 **커피와 차는 서브타입**이고 **음료는 슈퍼타입**이다.  

![subtype_supertype.png](/assets/attachment/kotlin_study/subtype_supertype.png){: width="400" height="400" }

**서브타입은 슈퍼타입의 특성과 동작 규칙을 상속**받으며, **슈퍼타입은 서브타입이 따라야하는 특성과 동작 규칙을 정의**한다.
> 모든 음료는 색을 가지고 있는 특징이 있으나, 커피와 차는 서로 다른 색을 가진다.

Kotlin에서의 모든 클래스는 `Any`는 슈퍼타입으로 모든 클래스는 `Any`를 상속받는다.
`Any`의 서브타입으로는 `Int`, `String`, `Double` 등이 있다.

### **예외 계층 구조의 개요**

예외도 마찬가지로 서브타입-슈퍼타입의 관계를 가지고 있다.
다음은 예외 계층 구조를 단순화하여 나타낸 것이다.

![throwable_supertype.png](/assets/attachment/kotlin_study/throwable_supertype.png){: width="400" height="400" }

가장 위에 위치하고 있는 `Throwable`은 Kotlin에서 발생하는 예외의 슈퍼타입이다.

다음은 `Throwable`의 두 가지 주요 서브타입이다.
- **오류(error)**
  - 프로그램이 처리 할 수 없는 심각한 문제이다.
  - 일반적으로 시스템 수준에서 발생하며, 코드에서 직접 처리할 수 없다.
    - 메모리 부족, 스택 오버플로 등이 있다.
- **예외(exception)**
  - 일반적인 예외 처리가 필요한 경우이다.
  - 애플리케이션 개발 중 발생하는 오류를 처리하는 데 사용된다.
  - 대부분의 예외는 Exception을 상속 받는다.
  - `RuntimeException`과 `IOException` 같은 예외들을 포함한다.

다음으로 몇 가지 예외에 대해여 다루어 보고자 한다.

#### **런타임 예외**
런타임 예외(`RuntimeException`)은 `Exception`의 특수한 서브 타입으로 프로그램 실행 중(`runtime`)에 발생할 수 있는 예외를 설명한다.  
런타임 예외는 대부분 **코드 검증 부족으로 인해 발생하며, 적절한 코드 작성으로 예방할 수 있다.**

다음은 주요 런타임 예외의 서브타입들이다.

![runtime_exception.png](/assets/attachment/kotlin_study/runtime_exception.png){: width="700"}

##### **산술 예외**
산술 예외(`ArithmeticException`)은 잘못된 산술 연산이 수행될 때 발생하는 예외이다.  

가장 대표적인 예시는 0으로 나누기 연산이다.

```kotlin
val example = 2 / 0
```

0으로 나누는 연산은 허용되지 않기 때문에 `ArithmeticException`가 발생하고 프로그램 실행이 중단된다.

##### **숫자 형식 오류**
숫자 형식 오류(`NumberFormatException`)은 숫자로 변환할 수 없는 값을 `Int` 또는 `Double`과 같은 숫자 타입으로 변환하려고 하면 발생한다.  

대표적인 예시는 문자열을 숫자로 변환하는 것이다.

```kotlin
val string = "It's not a number"
val number = string.toInt()
```

##### **인덱스 초과 예외**
인덱스 초과 예외(`IndexOutOfBoundsException`)은 `Array`나 `List`에서 존재하지 않는 인덱스에 접근할 경우 발생하는 예외이다.  

대표적인 예시는 다음과 같다.

```kotlin
val sequence = "string"
println(sequence[10000000])
```

- - -
## 예외 다루기

이제 예외가 어떤 것이며, 어떤 이유로 어떤 유형의 예외가 발생하여 프로그램을 중단 시킬 수 있는지 알게 되었다.  
또한, 예외가 어디에서 발생했는지 찾는 방법도 알고 있다.

따라서, **예외 발생 예시와 함께 이를 방지하는 방법과 개발자가 직접 예외를 발생시키는 방법을 통해 예외를 다루는 방법을 알고자 한다.**

### **예외 발생 예시**

다음 코드를 살펴보자.

```kotlin
fun calculateSpentMoney(total: Int, itemPrice: Int): Int {
    val amountToBuy = total / itemPrice // 최대 구입할 수 있는 개수를 반환
    return amountToBuy * itemPrice      // 최대 구입 개수를 구매하였을 때 최종 가격을 반환
}
```

위 프로그램은 상품의 현재 가지고 있는 금액에서 단일 상품을 최대로 구입하였을 때의 가격을 반환하는 프로그램이다.  
예를 들어, 현재 `$37`을 가지고 있으며 햄버거 가격이 `$2`이면, 함수는 `$36`을 반환한다.

그러나, 무료로 제공되는 음식이 있는 경우에는 어떻게 될까?

즉, `itemPrice`가 0인 경우에, 이 함수는 무료로 무한정 물건을 받을 수 있지만 비용은 들지 않는다.  
그런데, 위 프로그램은 이러한 경우를 전혀 다루고 있지 않다.  

따라서 `calculateSpentMoney(37, 0)`을 호출하면 `ArithmeticException`이 발생하면서 프로그램이 중단된다.    
이러한 **특수한 경우를 엣지 케이스(edge case)**라고 한다.

이 경우, **상품 가격이 `$0`인 경우 `0`을 반환하도록 수정**해보자.

```kotlin
fun calculateSpentMoney(total: Int, itemPrice: Int): Int {
    if (itemPrice == 0) { // 상품 가격이 $0 인 경우에 대한 처리
        return 0
    }
    val amountToBuy = total / itemPrice
    return amountToBuy * itemPrice
}
```

### **예외를 직접 발생시키기**
어떠한 경우에는 프로그램을 계속 실행시키는 것보다 명확하게 예외를 발생시키는 것이 더 나은 선택이다.

- 보유하고 있는 금액이 음수인 경우.
- 아이템 가격이 음수인 경우.
- etc...

이제 예외를 발생시켜보자.  
`throw` 뒤에 예외 객체(`Exception`) 추가하면, 프로그램은 즉시 충돌하며 해당 예외 메시지를 출력한다.

```kotlin
fun calculateSpentMoney(total: Int, itemPrice: Int): Int {
    if (total < 0) { // 보유하고 있는 금액이 음수인 경우
        throw Exception("Total can't be negative") // throw 키워드를 사용하여 예외를 발생시킬 수 있다.
    }
    if (itemPrice < 0) { // 상품 가격이 음수인 경우
        throw Exception("Item price can't be negative")
    }
    if (itemPrice == 0) {
        return 0
    }
    val amountToBuy = total / itemPrice
    return amountToBuy * itemPrice
}
```

> **Exception(...)??**  
> 모든 예외는 특정한 계층 구조를 가진다.    
> `Exception`은 일반적인 예외 타입이며, 보다 구체적인 예외 타입들(`NumberFormatException`, `ArithmaticException`, etc ..)도 존재한다.    
> 다양한 예외 타입을 활용하여 문제의 원인을 더욱 명확하게 나타낼 수 있다.
{: .prompt-tip}

> **예외 객체를 변수에 저장하기**
> 
> 예외도 객체(object)이기 때문에 변수에 저장할 수 있다.  
> 
> ```kotlin
> val countError = Exception("Number is too big")
> ```
> 
> 변수에 예외를 할당한 뒤 `throw` 구분에 변수를 할당하여 프로그램 중단을 일으킬 수 있다.
{: .prompt-tip}

> **예외를 발생시키는 함수의 반환 타입**  
> 예외를 발생키시는 함수의 반환 타입은 `Nothing`이다.    
> `Nothing`은 절대 값을 반환하지 않는 함수를 의미한다.  
{: .prompt-tip}

## **마치며,,**
- 컴파일 타임 오류 부터 특정 상황에 대한 예외를 발생시키는 방법까지 오류와 예외에 대해 전반적으로 알아보았다.
- 프로그램이 중단 되었을 때의 문제점이 오류인지 예외인지 명확히 구분하는게 중요하다고 느꼈다.
- 서브타입-슈퍼타입의 개념을 알게되었다.

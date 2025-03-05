---
title: "[Introduction to Kotlin] 함수 선언하기"
date: 2025-02-28 10:00:00 +0900
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

## **함수 선언하기**
Kotlin에서 함수(function)는 코드의 기본 구성요소로, **코드를 실행하고 재사용 할 수 있도록 정의된 블록**이다.  
함수는 일련의 명령어들을 묶어 실행할 수 있도록 만든 서브프로그램(subprogram)이라고 볼 수 있다.

함수는 코드를 청크(chunk)로 구성하기 때문에, **코드를 재사용 가능하게 하고, 중복을 줄이며, 가독성을 향상**시킨다.  
또한, 특정 작업을 함수 내부에 감싸면 보다 **모듈화되고 유지보수하기 쉬운 코드베이스(codebase)**를 구축할 수 있다.

> **코드베이스**는 시스템을 구성하는 모든 소스 코드의 집합이다.

### **기본 구문**
함수에는 이름이 있으므로 필요할 때 호출하여 사용할 수 있다.
> Kotlin 표준 라이브러리에는 기본적인 함수가 이미 많이 존재하므로 이를 이용하자.

새 함수를 선언하려면 키워드와 함수 이름, 괄호 안에 매개변수 목록, 결과 값의 유형을 지정해야한다.
```kotlin
fun functionName(param1: Type1, param2: Type2, ...) {
    // 함수 본문
    return result
}
```
함수의 구성요소는 아래와 같다.
1. 이름: 변수 이름과 동일한 규칙과 권장 사항을 따르는 이름.
2. 매개변수(parameter): 콜론으로 구분된 매개변수와 타입.
3. 반환 타입(return type): 반환 값이 없는 경우에는 생략 가능함.
   - `Int`, `Double`, `Boolean`, `String` 등
4. 본문(body): 함수가 수행하는 기능.
5. `return` 키워드: 반환값이 있는 경우에 필수로 작성해야함.

### 예제) 간단한 함수 정의하기
정수의 합을 계산하여 반환하는 함수를 정의해보자.

```kotlin
fun sum(a: Int, b: Int): Int {
    val result = a + b
    return result
}

fun main() {
    val result1 = sum(2, 5)
    println(result1) // 7
    
    val result2 = sum(result1, 10)
    println(result2) // 17
}
```

> 함수의 인수는 함수 내에서만 접근할 수 있다.  
> 즉, `sum` 함수의 `a`와 `b`는 함수 외부에서 직접 접근할 수 없다.

### **함수의 매개변수**
함수의 매개변수는 함수가 필요로 하는 입력값(input)을 나타낸다.
```kotlin
// 1. 입력 받은 값을 그대로 반환
fun identity(a: Int): Int {
    return a
}

// 2. 두 개의 정수를 더한 값을 반환
fun sum(a: Int, b: Int): Int {
    val result = a + b
    return result
}

// 3. 항상 3을 반환
fun get3(): Int {
    return 3
}

// 4. 다른 함수를 호출하여 계산
fun add3(a: Int): Int {
    return identity(a) + get3()
}

fun main() {
    println(identity(1000)) // 출력: 1000         
    println(sum(200, 300))  // 출력: 500    
    println(get3()) // 출력: 3
    println(add3(5))    // 출력: 8         
}
```

### **반환 타입**
함수는 단일 값을 반환하거나 아무것도 반환하지 않을 수 있다.  
함수가 무언가를 반환해야하는 경우에는 `return`키워드를 사용해야한다.

**반환 값이 없는 함수**
```kotlin
// 반환 타입을 생략 -> Unit 타입으로 반환됨.
fun printAB(a: Int, b: Int) {
    println(a)
    println(b)
}
// Unit을 명시적으로 지정(동일한 결과)
fun printSum(a: Int, b: Int): Unit {
    println(a + b)
}
```

### **함수 본문**
함수 본문은 함수 그 자체의 기능이며, 함수 내부에서만 접근 가능한 변수를 선언가능하다.  
> 마치 `main()`와 같이.

숫자를 받아 마지막 자리 숫자만 반환하는 함수 예시
```kotlin
fun extractLastDigit(number: Int): Int {
    val lastDigit = number % 10
    return lastDigit
}
```

위 함수를 아래와 같이 단순하게 작성할 수 있다.
```kotlin
fun extractLastDigit(number: Int): Int {
    return number % 10
}
```

주의할 점으로 함수는 `return` 이후의 코드는 실행되지 않는다.
```kotlin
fun getGreeting(): String {
    return "hello"
    println("hello") // Unreachable(도달할 수 없는 코드) 경고 발생함.
}
```

### **단일 표현식 함수**
만일 함수의 반환식이 한 줄로 표현된다면, 중괄호(curly braces)를 사용하지 않고 작성 가능하다.  
이를 단일 표현식 함수(single-expression functions)라고 한다.

```kotlin
fun extractLastDigit(number: Int): Int = number % 10

// 타입 추론으로 반환 타입이 자동 추론되므로 반환 타입을 작성하지 않아도 가능하다.
fun getGreeting() = println("Hello")
```



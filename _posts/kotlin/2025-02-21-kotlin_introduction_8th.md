---
title: "[Introduction to Kotlin] 사용자로부터 입력값 받기"
date: 2025-02-21 10:00:00 +0900
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

## **readln을 사용하여 데이터 읽기**
위 주제에서는 사용로부터 입력을 받아서 활용하는 방법을 배운다.  
대부분의 프로그램은 사용자로부터 특정 정보를 요청하는 경우가 있는데,  
Kotlin에서는 `readln()` 함수를 이용하여 변수를 다루는 방법과 다양한 데이터를 처리하는 방법을 알아본다.

### **표준 입력**
표준 입력(standard input)은 프로그램으로 들어가는 데이터스트림(data stream)이다.  
운영체제에서 이를 지원하며, 일반적으로 키보드에서 데이터를 받는다.

> 파일에서도 데이터를 받을 수 있다.

모든 프로그램이 표준 입력을 사용하는 것은 아니지만,  
일반적으로 표준 입력으로 프로그래밍 문제를 해결하는 과정은 아래와 같다.

1. 표준 입력으로부터 데이터를 받는다.
2. 데이터를 처리하여 결과를 얻는다.
3. 표준 출력(standard output)에 결과를 출력한다.

따라서, 데이터를 처리할 수 있는 유용한 프로그램을 만들기 위해서는 데이터를 읽는 방법부터 알아야한다.

### **readln() 사용법**
Kotlin에서는 `readln()` 함수로 표준 입력을 받을 수 있으며, 함수는 입력을 한 줄을 문자열로 읽는다.

```kotlin
val line = readln() // 문자열 반환
```

#### **Kotlin 이전 버전과의 차이점**
Kotlin 1.6 이전 버전을 사용하면 `readln()` 대신 `readLine()!!`을 사용해야한다.

```kotlin
val line = readLine()!!
```
여기서 느낌표 2개(!!) 연산자는 입력값이 절대 절대적으로 `null` 값이 아닌 것을 보장하는 연산자이다.

> 추후 이러한 연산자를 다루도록 한다.

#### **숫자 입력 받기**
**사용자로부터 숫자 입력을 받고 싶은 경우에는 타입 변환을 활용**하면 된다.

```kotlin
val number = readln().toInt()
println(number)

val bigNumber = readln().toLong()
println(bigNumber)
```

#### **실수 및 불리언 입력 받기**
마찬가지로 타입 변환을 활용하면 된다.

```kotlin
val double = readln().toDouble()
println(double)

val bool = readln().toBoolean()
println(bool)
```

#### **여러 개의 입력값 처리**
여러개의 데이터를 입력 받기 위해서는 각 변수를 선언하고 `readln()`을 여러번 호출하면 된다.
```kotlin
val a = readln()
val b = readln().toInt()
val c = readln()
print(a)
print(b)
print(c)
```

#### **한 줄에서 여러 값 입력받기**
**하나의 줄에서 공백으로 구분된 여러 개의 값을 저장하려면, `split("")`을 사용**하면 된다.
```kotlin
val (a, b) = readln().split(" ")
println(a)
println(b)
```




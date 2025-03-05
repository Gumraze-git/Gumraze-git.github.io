---
title: "[Introduction to Kotlin] IF 문"
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

## **If 표현식**
Kotlin의 조건식(conditional expressions) 중 `if` 표현식의 다양한 형태와 표현식 스타일(expression-style)로서의 활용법을 다뤄보고자 한다.  

### **조건식**
조건식(conditional expressions)는 `Boolean`의 값에 따라 다른 연산을 수행할 수 있도록 하는 기능이다.  
조건식에는 다양한 형태가 있으며, 대표적으로 다음과 같은 유형이 있다.
1. 단순 if 문(single if case)
2. if-else문(if-else cases)
3. if-else-if문(if-else-if cases)
4. 중첩 if문(Nested if's)

### **표현식 스타일의 if**
다른 일부 프로그래밍 언어와 다르게, Kotlin의 `if`는 표현식(expression)이며, 문장(statement)가 아니다.  
즉, if문이 계산 결과를 반환할 수 있으며, 해당 결과를 변수에 저장할 수 있다.  

```kotlin
val max = if (a > b) {
    println("Choose a")
    a
} else {
    println("Choose b")
    b
}
```
`if`문이 값(a or b)을 반환하고, 반환된 값이 `max` 변수에 저장이 된다.  
> 또한, 표현식 스타일의 `if`를 사용할 경우 반드시 `else` 블록이 있어야한다.

**단순 if 표현식**은 중괄호를 사용하지 않고 표현하는 방식이다.
```kotlin
val max = if (a > b) a else b
```
이는 if-else 블록이 단일 문장일 경우 코드를 더 간결하게 하기 위해 사용 가능하다.

변수 없이 `if` 표현식을 사용할 수도 있다.
```kotlin
fun main() {
    val a = readln().toInt()
    val b = readln().toInt()
  
    println(if (a == b) {
        "a equal b"
    } else if (a > b) {
        "a is greater than b"
    } else {
        "a is less than b"
    })
}
```
위와 같은 경우에는 별도의 변수를 선언하지 않고 함수인 `println()`에 바로 전달했다.

### **관용적 표현**
**결과를 반환해야 하는 경우**에는 **표현식 스타일에 if를 사용하는 것이 좋다**.  
이러한 경우에는 변수를 변경해야하는 실수나, 수정이 누락되는 문제를 방지할 수 있다.

```kotlin
val max = if (a > b) a else b
```

- - -
## **when: if의 강력한 대체재**
Kotlin에서는 `if-else-if` 체인을 대체할 수 있는 더 강력하고 표현력 있는 방법으로 `**when**`표현식을 제공한다.  
`when`표현식을 사용하면 여러 조건을 더 쉽게 처리할 수 있으며, 코드의 가독성을 높일 수 있다.  

아래는 `when` 표현식의 기본 예제이다.  
```kotlin
val number = 5

when (number) {
    1 -> println("One")
    2 -> println("Two")
    3 -> println("Three")
    4 -> println("Four")
    else -> println("Number is greater than four")
}
```
`when` 표현식은 주어진 변수(number)의 값을 확인하고, 일치하는 경우 해당 코드 블록을 실행한다.
> `else`는 말 그대로 나머지 경우의 처리를 수행한다.

### **when을 표현식으로 사용하기**
Kotlin의 `when`은 표현식으로도 사용 가능하며, 결과 값을 반환할 수 있다.  

```kotlin
val number = 3
val message = when (number) {
    1 -> "One"
    2 -> "Two"
    3 -> "Three"
    else -> "Number is greater than three"
}
```

### **when을 범위 및 조건과 함께 사용**
`when`은 범위(range) 및 복잡한 조건과도 함께 사용할 수도 있다.

```kotlin
val number = 15
when {
    number < 0 -> println("Negative number")
    number in 1..10 -> println("Number between 1 to 10")
    number % 2 == 0 -> println("Even number")
    else -> println("Odd number greater than 10")
}
```

`when`에서 변수를 직접 비교하지 않고, 조건을 평가할 수도 있다.  

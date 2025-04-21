---
title: "[Introduction to Kotlin] 구조적 동등성과 참조적 동등성"
date: 2025-04-18 10:00:00 +0900
layout: post
category: [Kotlin]
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Equality!
pin: false
---
- - -

## 구조적 동등성과 참조적 동등성
객체(object)는 복잡한 구조를 가지며, 변수는 단순히 객체를 가리키는 역할을 한다는 것을 알고 있다.  

객체 간의 동등성(equality)를 판단하는 방법과, 변수가 동일한 객체를 가리키는지 확인하는 방법을 배우게 된다.  
또한, `val` 키워드의 진정한 의미를 완전히 이해하고, **많은 초보자가 "val이 불변성을 보장한다"는 잘못된 가정을 피할 수 있다.**

### 구조적 동등성 예제
친구에게서 두 개의 동일한 메시지를 받았다고 가정해보자.  
두 개의 메시지는 `Hi`와 `Hi`로 같아 보인다.  

이 메시지를 Kotlin에서 비교하려면 **문자열(String) 변수**로 저장 후 `=` 연산자로 비교가 가능하다.

```kotlin
val msg1 = "Hi"
val msg2 = "Hi"
println(msg1 == msg2) // true
println(msg1 == "Hello") // false
```

비교 결과 `msg1`과 `msg2`는 동일한 내용을 가지고 있으므로 `true`가 출력된다.  
이와 같이 객체의 내부 상태(`state`)가 동일할 때 이를 구조적 동등성(structural equality)라고 한다.

> 일부 복잡한 데이터 타입은 `==`연산자를 지원하지 않을 수도 있다.

다음 예제는 공(ball)을 담을 수 있는 `Box` 객체가 있다.  
```kotlin
val blueBox = Box(3) // 공이 3개 있는 박스
val azureBox = blueBox // blueBox를 복사
println(blueBox == azureBox) // true

blueBox.addBall() // 공을 하나 추가
println(blueBox == azureBox) // true, 두 박스 모두 공이 4개가 있다.
```

`Box`에 공을 추가하게 되면 `blueBox`뿐만 아니라 `azureBox`도 변경이 된다.  
왜냐하면, `blueBox`와 `azureBox`는 같은 객체를 가리키고 있기 때문이다.  

> 여기서 `val`로 선언한 변수의 객체 상태가 변경이 되었다는 점을 알 수 있다.

### 참조적 동등성
객체가 동일한 상태(내용)을 가지고 있는 경우와 동일한 객체를 가리키는 경우를 구분하는 것이 필요하다.  
Kotlin에서는 `===`연산자를 사용하여 변수들이 같은 객체를 가리키는지 확인할 수 있다.  

```kotlin
val blueBox = Box(3)
val azureBox = blueBox
val cyanBox = Box(3)

println(blueBox == azureBox)  // true (내용이 같음)
println(blueBox === azureBox) // true (같은 객체를 가리킴)

println(blueBox == cyanBox)   // true (내용이 같음)
println(blueBox === cyanBox)  // false (다른 객체를 가리킴)
```

출력 결과에서 확일 할 수 있듯이, `blueBox`와 `azureBox`는 내용도 같고 같은 객체를 가리키지만,  
`blueBox`와 `cyanBox`는 내용이 같으나 다른 객체를 가리키고 있다.  

> 반대로 참조적 불일치를 확인하려면 `!==` 연산자를 사용하면 된다.  
> ```kotlin
> println(blueBox !== cyanBox) // true
> ```
{: .prompt-tip }

또한, `===` 연산자는 불변 객체(immutable object)에서도 흥미로운 특징을 가진다.  
```kotlin
var two = 2
var anotherTwo = 2

println(two === anotherTwo) // true

two ++
println(two) // 3
println(anotherTwo) // 2
println(two === anotherTwo) // false
```

`var` 유형의 변수에 객체를 할당 후 변경하면, 새로운 객체가 할당된다.  
따라서, 불변 객체는 여러 문제를 방지할 수 있다.

### 기본 타입과 동등성 비교
Kotlin에서는 기본 데이터 타입도 객체이다.

```kotlin
var a: Int = 100
val anotherA: Int = a

println(a == anotherA) // true
println(a === anotherA) // true

var d1: Double = 1.5
val d2 = d1
println(d1 === d2) // true
```

### 가변 객체에서의 문제
다음 예지를 살펴보자
```kotlin
val list1: MutableList<Int> = mutableListOf()
val list2: MutableList<Int> = list1

list1.add(1)
println("list1 $list1") // list1 [1]
println("list2 $list2") // list2 [1]

list2.add(5)
println("list1 $list1") // list1 [1, 5]
println("list2 $list2") // list2 [1, 5]
```

`list1`과 `list2`는 같은 객체를 가리키므로, 하나를 변경하면 다른 것도 영향을 받게 된다.  
이것이 가변 객체를 다룰 때 주의해야하는 이유이다.  


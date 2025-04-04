---
title: "[Introduction to Kotlin] 객체와 클래스의 상태 및 동작"
date: 2025-04-04 10:00:00 +0900
layout: post
category: [Kotlin]
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: objects are temporary, but classes are forever
pin: false
---
- - -
## **객체와 그 속성**
우리의 삶은 항상 객체(object)로 둘러싸여 있다.  
자동차를 운전하고, TV를 보고, 책을 읽고, 물건을 결제하는 등 다양한 객체를 일상적으로 사용한다.

프로그래밍 언어에서 **객체는 메모리의 한 부분을 차지하여 특정 정보를 저장**한다.    
**변수와 값은 단순히 객체를 가리키는 역할**을 하며, 우리는 **변수를 이용하여 객체와 작업**할 수 있게 된다.

### **객체의 상태와 동작**

우리는 객체의 다음 두 가지로 작업을 할 수 있다.
- 상태(state): 객체가 가지고 있는 데이터나 속성(property)  
  > 상태는 주로 `.property` 형태로 접근한다.
- 동작(behavior): 객체가 수행할 수 있는 기능이나 동작  
  > 즉, 함수나 메서드(method)를 의미하며, 주로 `.functionName()`으로 접근한다.

  
#### **예시) 문자열**
문자열 객체는 메시지를 저장하며, 다음과 같은 여러 가지 상태와 동작이 가능하다.

- **문자열의 상태**

| 상태           | 설명               | 예시                  |
|--------------|------------------|---------------------|
| length       | 문자열의 길이          | "Kotlin".length     |
| isEmpty()    | 문자열이 비어있는지 여부    | "".isEmpty()        |
| isNotEmpty() | 문자열이 비어있지 않은지 여부 | "".isNotEmpty()     |
| first()      | 첫 번째 문자          | "Kotlin".first()    |
| last()       | 마지막 문자           | "Kotlin".last()     |
| indices      | 인덱스 범위           | "Hi".indices → 0..1 |
| get[index]   | 특정 인덱스의 문자       | "abc"[1]            |


- **문자열의 동작**

| 상태                    | 설명               | 예시                        |
|-----------------------|------------------|---------------------------|
| repeat(n)             | 문자열을 n번 반복       | "Kotlin".repeat(3)        |
| uppercase()           | 문자열이 비어있는지 여부    | "".isEmpty()              |
| lowercase()           | 문자열이 비어있지 않은지 여부 | "".isNotEmpty()           |
| trim()                | 앞뒤 공백 제거         | "  Hi  ".trim()           |
| replace(old, new)     | 문자열 치환           | "apple".replace("a", "A") |
| substring(start, end) | 부분 문자열 반환        | "Kotlin".substring(0, 3)  |
| contains(str)         | 포함 여부 확인         | "hello".contains("e")     |
| startsWith(str)       | 특정 문자열로 시작하는지    | "Kotlin".startsWith("k")  |
| endsWith(str)         | 특정 문자열로 끝나는지     | "Kotlin".endsWith("n")    |
| split(delimiter)      | 구분자로 나누기         | "a,b,c".split(",")        |
| toCharArray()         | 문자 배열로 변환        | "abc".toCharArray()       |
| plus(str)             | 문자열 연결           | "Hi".plus(" there")       |

- **사용 방법은 다음과 같다.**

```kotlin
val msg = "Hi"
println(msg.length) // 2
```

```kotlin
val msg = "Hi"
println(msg.repeat(3)) // "HiHiHi"
```

### **참조에 의한 복사**
프로그래밍에서 **복사(copying)는** 일반적인 작업이며, **대부분의 경우 `=` 연산자를 사용하여 이루어진다**.  
Kotlin에서는 객체가 복사되는 방식은 **1개의 은행 계좌에서 여러 개의 카드를 가지고 결제를 하는 방식**으로 작동한다.

즉, **어떤 카드로 결제해도 같은 계좌에서 돈이 빠져나가는 것이다**.  
다음 예시를 살펴보자.

```kotlin
val msg1 = "Hi" // msg1에 Hi 할당
val msg1 = msg2 // msg2에 msg1 할당
```

위와 같은 경우에 `Hi` 객체가 복사되는 것이 아니라 `msg1`과 `msg2`는 같은 `Hi` 객체를 가리키게 된다.

![object_copy.png](/assets/attachment/kotlin_study/object_copy.png){: w="500"}

즉, **`=` 연산자는 객체 자체를 복사하는 것이 아니라**, **객체를 참조하는 주소(reference)를 복사**하는 것이다.

### **객체와 변경 가능성(mutability)**
**하나의 객체를 여러 개의 변수가 참조하고 있을 때**, 그 **객체를 어떻게 변경**하면 좋을까?  
이것은 **객체가 변경 가능한지(mutable)** 또는 **변경 불가능한지(Immutable)에 따라 다르다**.

#### **불변 객체: Int와 String**
Kotlin에서는 `Int`, `String`, `Float`, `Double`과 같은 기본 타입도 모두 객체이다.  
하지만, 이 **객체들은 불변으로 한 번 생성된 후에는 변경할 수 없다**.

두 변수가 가리키고 있는 객체가 동일한지 확인하기 위해 **참조 비교(reference equality)**를 할 수 있다. 

|연산자|의미|
|---|---|
|`==`| 값 비교(내용이 같은가?)|
|`===`| 참조 비교(같은 객체인가?)|

- **다음 예시를 확인해보자**

```kotlin
var a: Int = 100 // a에 100 할당
var anotherA: Int = a // anotherA에 a 할당
println(a == anotherA) // true
println(a === anotherA) // true

a = 200 // a에 객체 "200" 할당
println(a == anotherA) // false
println(a === anotherA) // false
```

![object_assignment.png](/assets/attachment/kotlin_study/object_assignment.png)
> 기존에 생성된 객체(100)는 변경되지 않으며, 새로운 객체(200)이 생성된 것이다.

- - -
## **클래스 선언하기**
프로그래머가 객체 지향 프로그래밍(OOP)를 구현할 때, 기존에 정의된 클래스를 활용하여 프로그램을 작성하게 되는 경우가 많다.
예시로, `Scanner` 클래스의 객체를 사용하면 콘솔 입력에서 단어를 읽을 수 있고 이 단어는 자체적으로 `String` 클래스의 객체이다.

하지만, 프로그래머는 프로그램에 특화된 새로운 클래스를 선언 할 필요가 있다.  
이번에는 **새로운 클래스를 선언하고 클래스 객체의 상태와 동작을 사용하는 여러 가지 방법**을 다뤄본다.

### **새로운 클래스 선언하기**
새로운 클래스를 선언하려면 `class` 키워드 뒤에 클래스 이름을 작성해야한다.  
먼저, `Emptiness` 라는 클래스를 선언해보자.

```kotlin
class Emptiness {
    // empty body
}
```

또한, 클래스는 `.kt` 파일 내에서 최상위(top-level)으로 선언하는 것이 일반적이다.
> ex) Emptiness.kt 내의 **최상위 클래스 Emptiness**가 있는 것이다.

### **객체, 클래스, 인스턴스의 개념**
앞에서 **객체**에 대해 다루었고, 다음으로 **클래스**와 **인스턴스(instance)**를 다루고자한다.  
클래스, 객체, 인스턴스는 OOP에서 가장 기본이 되는 개념이지만, 용어가 비슷해서 헷갈릴 수 있다.  
각각의 차이점을 알아보자.

![class_object_instance.png](/assets/attachment/kotlin_study/class_object_instance.png){: w="300" }

- **객체**
  - 객체는 메모리에 저장되어 있는 실체이며 상태와 동작을 가지고 있는 대상이다.
- **클래스**
  - 클래스는 객체를 만들기 위한 설계도이다.
  - 클래스 자체로는 메모리에 올라가지 않으며, 객체를 생성하기 위한 툴이다.
- **인스턴스**
  - 인스턴스는 클래스로 만들어낸 객체이다.
  - 인스턴스는 객체와 거의 같은 의미이지만, 어떤 클래스의 결과물인가?에 초점을 둔 표현이다.
    > 인스턴스는 항상 클래스와의 관계를 전제로 하는 용어이다.

### **인스턴스 생성하기**
클래스를 정의하여 새로운 데이터 타입을 만들 수 있고, 이를 기반으로 인스턴스를 생성할 수 있다.

기본 데이터 타입만으로는 표현이 어려운 경우가 많기 때문에 **사용자 정의 인스턴스를 생성하는 기능이 매우 유용**하다.
인스턴스를 생성하는 방법은 다음과 같다.

```kotlin
val empty: Emptiness = Emptiness()
```

`Emptiness` 클래스의 새로운 객체를 `empty` 변수에 할당했다.  
`empty` 변수의 타입은 `Emptiness`이므로, 다른 타입의 객체를 할당 할 수 없다.

### **클래스 속성**
클래스 본문에는 클래스 멤버(class member)인 속성을 추가할 수 있다.
속성은 Kotlin의 일반적인 변수 선언과 비슷한 방식으로 선언되나, **반드시 초기 값을 가져야 한다**.

```kotlin
class Patient {
    var name: String = "Unknown"
    var age: Int = 0
    var height: Double = 0.0
}
```

위 `Patient` 클래스는 이름(name), 나이(age), 키(height)를 속성으로 가지며,  
모든 속성은 `var`로 선언되어 인스턴스 생성 후 속성을 변경할 수 있다.

### **속성에 접근하기**
객체 이름 뒤에 점(.)을 이용하여 속성에 접근할 수 있다.

```kotlin
var patient = Patient()
println(patient.name) // "Unknown"
println(patient.age) // 0
```

`Patient` 클래스의 객체(`patient`)를 생성하면 모든 속성은 기본 값은 유지하고 있다.

### **속성 값 변경하기**
환자의 정보를 변경하는 예제를 확인해보자.  
두 명의 환자를 생성하고, 각자의 속성을 설정한 후 출력해보자.

```kotlin
class Patient {
    var name = "Unknown"
    var age = 0
    var height = 0.0
}

fun main() {
    val john = Patient()
    john.name = "John"
    john.age = 30
    john.height = 180.5
    
    val alice = Patient()
    alice.name = "Alice"
    alice.age = 20
    alice.height = 176.2
  
    println("${john.name}: ${john.age} yrs, ${john.height} cm")
    println("${alice.name}: ${alice.age} yrs, ${alice.height} cm")
}
```

**출력 결과**
```text
John: 30 yrs, 180.0 cm
Alice: 22 yrs, 165.0 cm
```

`john` 객체와 `alice` 객체는 각각 독립적인 속성 값을 가지게 된다.


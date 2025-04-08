---
title: "[Introduction to Kotlin] 클래스의 생성자 및 멤버 함수"
date: 2025-04-11 10:00:00 +0900
layout: post
category: [Kotlin]
comments: true
tag: [Kotlin, OOP]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Class members are important!
pin: false
---
- - -
## **생성자**
이미 속성이 간단한 클래스를 선언하는 방법은 알고 있다.  
이제 클래스 멤버(class member)의 다른 종류인 생성자(constructor)에 대해 알아보자.

> 클래스 멤버는 클래스 내부에 포함된 요소들로서,  
> 객체가 가질 수 있는 상태(데이터)와 동작(기능)을 정의한다.  
{: .prompt-tip }

### **기본 생성자**
생성자는 클래스의 객체를 초기화하는 클래스 멤버이다.  
다시 말해, 생성자는 새로운 객체의 상태를 설정하며 속성을 초기화한다.  
즉, 객체를 생성할 때 생성자를 호출하게 된다.

예시로 다음과 같은 클래스가 있다.
```kotlin
// 클래스 선언
class Size {
    var width: Int = 1
    var height: Int = 1
}
```

클래스의 인스턴스는 다음과 같이 선언한다.
```kotlin
// 객체 생성
val size = Size()
```

사실 이것은 생성자 호출이며, 인자가 없는 함수를 호출하는 것과 유사하다.  
모든 클래스는 생성자를 하나 이상 가져야 하므로, 생성자가 명시적으로 정의되지 않으면,  
컴파일러가 자동으로 인자가 없는 기본 생성자를 생성해준다.  


### **주 생성자**
객체를 생성하기 전에 그 객체가 가질 속성 값을 알고 있는 경우가 많다.  
이럴 때는 생성자에 인자를 넘겨 속성을 설정하면 코드가 더 간결해진다.  
이럴 때 **사용하는 것이 주 생성자(primary constructor)이다**.

주 생성자는 별도의 코드 블록 없이 클래스의 인스턴스와 속성만을 초기화한다.  
클래스 이름 뒤 `constructor` 키워드를 작성하고 초기화 인자를 넣으면 된다.

```kotlin
class Size constructor(width: Int, height: Int) {
    val width: Int = width
    val height: Int = height
    val area: Int = width * height
}
```

그러나 일반적으로 다음과 같이 `constructor` 키워드를 생략하여 작성한다.
```kotlin
class Size constructor(width: Int, height: Int) {
    val width: Int = width
    val height: Int = height
    val area: Int = width * height
}
```

### **주 생성자의 속성 선언**
주 생성자 괄호 안에 속성을 직접 선언할 수 있다.  

```kotlin
class Size(val width: Int, height: Int) {
    val height: Int = height
    val area: Int = width * height
}
```

`height`도 생성자 안으로 옮기면,
```kotlin
class Size(val width: Int, val height: Int) {
    val area: Int = width * height
}
```

### **기본 값과 명명된 인자**
Kotlin의 주 생성자에서는 클래스 본문처럼 기본값을 지정할 수 있다.  
```kotlin
class Size(val width: Int = 1, val height: Int = 1) {
  val area: Int = width * height
}
```

객체 생성 시 인자를 생략하면 기본값이 사용된다.  
```kotlin
val size = Size() // width == 1, height == 1, area == 1
```

클래스에 인자를 줄 때는 순서대로 줄 수도 있고, 명명된 인자(named argument)를 사용할 수도 있다.
```kotlin
val size1 = Size(3, 5)
val size1 = Size(width = 3, height = 5)
val size1 = Size( height = 5, width = 3)
```

> 일부 인자만 줄 경우, 순서를 지키지 않는다면 명명된 인자를 반드시 사용해야 한다.

### **한 줄짜리 클래스**
주 생성자 이외에 다른 클래스 멤버가 없다면 중괄호를 생략할 수 있다.
```kotlin
class Size(val width: Int = 1, val height: Int = 1)
```

### **init 블록**
**주 생성자는 코드 블록을 포함할 수 없다.**

하지만 생성 중 로직이 필요하다면, `init` 블록을 통해 초기화 로직을 실행 할 수 있다.
```kotlin
class Size(_width: Int, _height: Int) {
    var width: Int = 0
    var height: Int = 0
  
    init {
        width = if (_width >= 0) _width else {
            println("너비는 0 이상이어야 합니다.")
            0 // else인 경우 반환되는 값 = 0
        }
        height = if (_height >= 0) _height else {
            println("높이는 0 이상이어야 합니다.")
            0
        }
        
    }
}
```

또는 속성 설정 후 메시지를 출력하는 용도로도 사용된다.

```kotlin
class Size(val width: Int, val height: Int) {
    init {
        prinltn("초기화 블록 실행: width = $width, height = $height")
    }
}
```

여러 개의 `init` 블록도 사용할 수 있으며, 정의된 순서대로 실행된다.
```kotlin
class Size(_width: Int, _height: Int) {
    val width = _width
    init {
        println("첫 번째 init: width = $width")
    }

    val height = _height
    init {
        println("두 번째 init: height = $height")
    }

    val area = width * height
}
```

> 언더스코어(`_width`, `_height`)를 사용한 인자 이름은 속성과 구분하기 위한 코딩 관례이다.

- - -
## **멤버 함수**
객체에는 단순히 데이터뿐만 아니라 동작(행동)도 저장해야할 필요가 있다.  
멤버 함수는 동일한 클래스에 속한 객체들 전체에 공통적인 동작을 구현한다.  

멤버 함수는 클래스 본문 안에 정의된 함수처럼 보이며,  
다음 예시에서는 `print()`라는 함수를 가진 클래스를 선언하고 있다.  
```kotlin
class MyClass {
    fun print() = println("Hello from print")
}
```

위 함수는 **특정 클래스의 객체와 함께 작동**하고 **해당 객체의 필드에 접근**할 수 있기 때문에 **멤버 함수(member function)이라고 불린다**.
> 일반적으로는 메서드(method)라고 불리우나, Kotlin 공식 문서에서는 멤버 함수라고 부른다.   

다음 예시에서 `this` 키워드는 현재 클래스의 인스턴스를 나타낸다.
```kotlin
class MyClassWithProperty(var property: Int) {
    fun printProperty() {
        println(this.property)
    }
}
```
> `this`를 생략해도 되며, 선택사항이다. 

일반 함수처럼 멤버 함수도 인자를 받을 수 있으며, 정의된 클래스 타입을 포함한 모든 타입의 값을 반환할 수 있다.  

### **멤버 함수 호출하기**
다음 예시는, 특정 객체의 필드 값을 출력하는 멤버 함수를 호출한다.
```kotlin
val myObject = MyClassWithProperty(10)
myObject.printProperty() // "10" 출력
```

멤버 함수는 클래스의 객체 이름 뒤에 마침표(`.`)를 찍어 호출 및 사용할 수 있다.  

### **예제) 고양이**
멤버 함수를 사용하는 예제를 살펴보자.

고양이 클래스는 다음과 같이 행동할 수 있다.
- 고양이는 두 가지 상태를 가지며, 상태에 따른 소리를 낸다.
  - 잠자는 상태, `zzz`
  - 깨어있는 상태, `meow`

```kotlin
import kotlin.random.Random // 랜덤 숫자 생성

class Cat(val name: String) {
    var sleeping: Boolean = false // 고양이의 현재 상태, 기본값은 자고 있지 않음
    
    fun say() {
        if (sleeping) {
            println("zzz")
        } else {
            println("meow")
            
            if (Random.nextDouble() < 0.1) { // 0과 1사이의 난수 생성
                sleeping = true
            }
        } 
    }
  
    fun wakeUp() { // 고양이를 깨우는 함수
        sleeping = false
    }
}
```

이제 클래스의 인스턴스를 생성하여 고양이를 호출해보자.
```kotlin
fun main() {
    val pharaoh = Cat("Pharaoh")
    
    repeat(5) {
        pharaoh.say() // "meow" 또는 "zzz" 출력
    }
    
    pharaoh.wakeUp() // 고양이 깨우기
    pharaoh.say() // 다시 meow 출력
}
```

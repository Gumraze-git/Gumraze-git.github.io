---
title: "[Introduction to Kotlin] 변수, 데이터 타입, 주석"
date: 2025-01-04 21:00:00 +0900
layout: post
category: Kotlin
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Introduction for Basic Kotlin
pin: false
---

- - -
## **시작하면서,,**
현재 HyperSkill을 통해 Kotlin을 공부하고 있는데, 초보 개발자들이 개발에 대해 접근하기 쉽도록 커리큘럼이 잘 구성되어 있다는 느낌을 받았다.
따라서, 처음 개발을 kotlin으로 공부하고자 하는 분들에게 추천하고 싶다.

그러나 강의 내용이 영어로 작성되어 있어 아무래도 영어가 친숙하지 않은 분들에게는 어려울 수 있다.
> **"아니 코딩도 어려운데 읽이 어려운 영어도 번역해가면서 읽어야해??"**

하지만, **아이러니하게 코드는 영어로 작성한다.**

어차피 영어와 멀어질 수 없으니 편안한 마음으로 공부하면 좋을 것 같다.

> 여담으로, 한글을 베이스로 하는 말씨, 씨앗 등의 프로그래밍 언어들도 있다.  
> 그리고 엄랭이라는 재미있는 프로그래밍 언어도 있는데, 이것은 시간이 나면 한 번씩 보면 좋을 것 같다.  
> 엄랭 보러가기 -> [엄랭 어떤 놈이 만들었냐? 어떤 놈 만났습니다.](https://youtu.be/NS56sb6EYIw?si=JFTyvSBRQZJEgWj8)

지난번 Kotlin에 대한 간단한 역사와 basic syntax에 대해 알아보았다.  
이번에는 더욱 간단하게 **변수(variable), 데이터 타입 그리고 주석(comments)**에 대해 공부한 것을 공유하고자 한다.

> 본 내용은 HyperSkill의 내용을 번역 및 의역하였으며, 공부하면서 일부 수정되고 생략된 내용이 있습니다.
{: .prompt-info }

- - -
## **What is a Variable: 변수란?**
변수는 어떠한 값을 저장하는 객체로 문자열(string), 숫자(number) 등을 저장하는 곳이다.

변수의 특징은 아래와 같다.
- 모든 변수는 다른 변수와 구별하기 위한 이름인 식별자(identifier)가 있다.
- 변수의 이름으로 값에 접근할 수 있다.

변수는 프로그램에서 자주 사용되는 요소 중 하나로 Kotlin에서의 변수 사용법을 이해하는 것이 중요하다.

### **Declaring variable in Kotlin: Kotlin에서 변수 선언하기**

**Kotlin에서는 변수를 선언하기 위해 대표적으로 두 가지 `val`과 `var` 키워드를 사용한다.**  
이외 `const val`을 이용하여 컴파일 시점에 결정되는 상수에 관한 변수를 선언한다.

#### **val(value)**
- `val`은 읽기 전용(read only) 변수로 명명된 값(named value)을 선언한다.
- 이 변수는 초기화된 후 변경이 불가능하여, **한 번만 값을 할당할 수 있다**.
     > 무조건적으로 한 번만 할당할 수 있는 것은 아니다.
- **사용 예시**

   ```kotlin
   val language = "Kotlin"
   println(language) // 출력 결과: Kotlin
    
   language = "Python" // 에러 발생, val은 변경 불가능함.
   ```

   ```kotlin
   val boolFalse: Boolean // Boolean으로 변수의 데이터 타입 선언
   println(boolFalse) // 에러 발생, 불린이 할당되기 전에 사용됨.
   ```

   ```kotlin
   val boolFalse: Boolean // Boolean으로 변수의 데이터 타입 선언
   boolFalse = false // 값 초기화(선언)
   println(boolFalse) // 출력 결과: false
   ```

#### **var(variable)**
- 필요한 만큼 변경가능한(mutable) 변수를 선언한다.
- **사용 예시**

   ```kotlin
   var language = "Kotlin"
   println(language) // 출력 결과: Kotlin
   
   language = "Python" // var은 변경가능한 변수임.
   println(language) // 출력 결과: Python
   
   language = 10 // 에러 발생, var은 초기 값과 동일한 유형의 값으로만 변경 가능함.
   ```

#### **변수 `val`과 가변성(mutable)**
`val`은 불가변성(immutable)의 동의어가 아니다.
`val`으로 변수가 선언되었더라도 참조된 객체가 가변(mutable)이면 객체의 내부 상태를 변경할 수 있다.

1. 가변 객체를 참조하는 경우
   `val`로 선언된 변수는 참조(reference)를 변경할 수 없지만, 참조하는 객체가 가변(mutable) 타입인 경우에는 객체의 내부 상태를 변경할 수 있다.

    ```kotlin
    val list = mutableListOf(1, 2, 3) // val로 선언된 가변 리스트
    list.add(4) // 리스트에 값 추가
    println(list) // 출력 결과: [1, 2, 3, 4]
    
    list = mutableListOf(1, 2, 3, 4, 5) // 컴파일 오류: 참조 자체를 변경 불가함.
    ```

2. 클래스 내부의 변경 가능한 속성이 있는 경우
   `val`로 선언된 객체의 속성이 가변(`val`)인 경우 해당 값을 변경 시킬 수 있다.

    ```kotlin
    class Person(var name: String, var age: Int)
    
    fun main() {
      val person = Person("Gumraze", 15) // 클래스 선언
      println(person.name) // 출력 결과: Gumraze
      println(person.age) // 출력 결과: 15
      
      // 객체의 속성 변경
      person.name = "Kim"
      person.age = 20
      
      println(person.name) // 출력 결과: Kim
      println(person.age) // 출력 결과: 20
    }
    ```
> Java에 익숙하다면, `val`은 Java의 `final`변수와 동일하게 취급하면 된다.  
> 이 둘은 매우 유사한데, 모두 변수에 값을 다시 할당하는 것은 금지하지만 객체의 내부 상태는 변경할 수 있다.

#### **const(constant) val**
`const val`은 컴파일 시점에 확정되는 값으로 변수를 선언할 때, 초기값이 지정되어야한다.  
변수의 값은 컴파일 시점에 결정되므로 런타임 도중에는 변경되지 않는다.

- **사용 예시**
  - 변수의 값은 컴파일 타임에 결정되며 런 타임에는 변경되지 않음.
    ```kotlin
    const val PI = 3.14159  // 컴파일 시점에 값이 결정됨.
    val PI = 3.14159 // 동일하게 가능함.
    ```
  - 아래 코드는 프로그램 실행 후 결정되는 값(상수가 아님)이므로 오류가 발생함.
    ```kotlin
    const val MY_STRING = readln() // 에러 발생
    ```
  >   상세한 내용은 다음 [출처](https://itstory1592.tistory.com/104) 참고 바랍니다.

- `const` 변수는 함수 밖의 최상위 수준에서 선언되어야 한다.
  ```kotlin
  const val MAX_USERS = 100  // 최상위 수준에서 선언
  const val APP_NAME = "MyApplication"
  
  fun main() {
      println("App Name: $APP_NAME")
      println("Max Users: $MAX_USERS")
  }
  ```

#### **Naming Convention: 이름 명명 규칙**
Kotlin에서 `val`과 `const`를 선언할 때에는 쉽게 작성가능하고 유지할 수 있는 명명 규칙이 있다.

- `val`의 경우에는 `camelCase`를 사용한다.
  ```kotlin
  val numberOfWheels: Int
  val isConnetionAvailalbe: Boolean
  val userFirstName: String
  ```
- `const` 변수는 컴파일 타임 상수이다.
- 변수는 정적이고 변경 불가능한 값을 나타내므로 이름은 대문자이어야 하며 밑줄로 단어를 구분해야한다.
  ```kotlin
  const val MAX_USER_COUNT = 50
  const val COMPANY_NAME = "TechCorp"
  const val VERSION_CODE = 3
  ```

#### **변수 사용 주의사항**
- 변수 이름은 숫자로 시작할 수 없다.
- 변수 이름은 의미있고, 이해하기 쉬우며, 읽기 쉬운 이름을 선택해야한다.
  - 변수가 복잡한 역할을 하여 이름을 설정하는 것의 어려움이 있다면 변수 이름이 길어지더라도 작성하는 것이 좋다.
- 많은 경우 불변 변수(`val`)으로 변수를 선언하는 것이 더욱 좋다.
  - 코드에 가변 변수가 많을수록 코드를 읽고 이해하는 것이 어렵다.


## **Data Type**
숫자는 산술 연산이 가능하고, 텍스트에서는 산술 연산(arithmeice operation)이 불가능하다.
> 자명하다.

Kotlin 뿐만 아니라 많은 프로그래밍 언어에서는 모든 변수에는 해당 변수에서 수행할 수 있는 연산과 저장할 수 있는 값을 결정하는 데이터 타입이 존재한다.

### **Vairable types: 변수의 형식**
- 변수의 타입은 변수가 선언될 때 결정된다.
  ```kotlin
  val text = "Hello, I'm studying Kotlin" // String
  val n = 1 // Int
  ```
  
  위의 경우, Kotlin은 text 변수가 문자열(String)이고, n이 숫자(number)인 것을 알고 있다.  
  Kotlin은 타입 추론(type inference)을 통해 타입을 자동으로 결정하는 매커니즘을 가지고 있다.

- 변수를 선언할 때 타입을 명시적으로 지정할 수도 있다.
  ```kotlin
  val text: String = "Hello, I'm studying Kotlin"
  val n: Int = 5
  ```
  > Type은 항상 대문자로 작성되어야 한다.
  {: .prompt-info }

  **타입 추론을 사용하면 코드가 간결하고 가독성이 증가**하지만, **경우에 따라 타입을 명시하는 것이 더 좋을 수 있다**.  
  그 예시로 변수를 선언한 뒤 나중에 초기화해야 하는 경우에는 타입 추론이 작동하지 않는다. 

  - 에러 발생
    ```kotlin
    val greeting // 에러 발생
    greeting = "Hello"
    ```

  - 정상 작동
    ```kotlin
    val greeting: String // OK
    greeting = "Hello"
    ```

### **Type mismatch**
데이터 타입의 중요한 기능 중 하나는 변수에 부적절한 값을 할당하지 못하도록 보호하는 것이다.

```kotlin
val n: Int = "abc" // 타입 불일치: 추론된 타입은 String이지만, Int가 필요하다.
```

타입 불일치 오류가 발생하면, 변수에 부적절한 값을 할당했음을 의미한다.  
또한, 타입 추론으로 선언된 가변 변수(mutable variable)에도 동일한 문제가 발생할 수 있다.

```kotlin
var age = 30 // 타입이 Int로 추론되었다.
age = "31 years old" // String이 입력되어 에러 발생
```

> 한번 선언된 변수의 타입은 변경할 수 없다.
{: .prompt-warning }

## **Comment(주석)**
주석은 컴파일러가 무시하는 텍스트이며, 이를 이용하여 코드의 일부를 설명하거나 코드를 제외(비활성화) 하는데 사용된다.

Kotlin에는 3가지 종류의 주석이 있는 본 섹션에서는 주석을 활용하여 코드가 어떻게 그리고 왜 작동하는지 설명한다.

### **End-of-line comments(한 줄 주석)**
`//` 뒤에 오는 텍스트 및 코드는 해당 줄에서 컴파일러에 의해 무시된다.

```kotlin
fun main() {
  // 아래 줄은 무시됩니다.
  // println("Hello")
  
  // 아래 코드는 "Hello Kotlin"을 출력합니다.
  println("Hello Kotlin")
}
```
> [TIP] 대부분의 코드 에디터에서는 `Ctrl + /` 또는 `Cmd + /`을 눌러 한 줄을 주석 처리할 수 있다.

### **Multi-line comments(여러 줄 주석)**
`/*`와 `*/` 사이에 있는 모든 텍스트는 컴파일러에 의해 무시된다.  
이를 단일 줄 주석이나 여러 줄 주석에 사용할 수 있다.

```kotlin
fun main() {
  /*
  여러 줄 주석의 예시
  println("Hello")
  println("World")
   */
}
```

### **Nested Comments(중첩 주석)**
여러 줄 주석은 다른 주석 안에 중첩될 수 있다.  
그러나, 중첩된 주석을 작성할 때는 `/*`와 `*/`가 반드시 쌍을 이루도록 작성해야한다.
```kotlin
fun main() {
  /*
  println("Hello") // Hello 출력
  println("Kotlin") // Kotlin 출력
   */
}
```

### **Documentation Comments(doc comments, 문서화 주석)**
`/**`와 `*/` 사이의 텍스트는 여러 줄 주석처럼 무시된다.  
그러나 이 주석은 문서화 주석이라고 불리우며, 코드의 동작을 이해하는데 도움을 주는 텍스트이다.  
```kotlin
/**
 * `main` 함수는 외부에서 문자열 인수를 받는다.
 * 
 * @param args 명령줄에서 전달된 인수들.
 */
fun main(args: Array<String>) {
  // do something
}
```

### **주석의 사용**
주석은 현명하게 사용되어야한다.
수많은 주석이 프로그램을 명확하게 만드는 것이 아니기 때문이다.

코드는 변경될 수 있고, 주석은 그 과정에서 오래되어 부정확할 수 있기 때문이다. 
따라서 항상 **자체적으로 문서화되는 코드(self-documenting code)를 작성하는 것이 중요**하다.

## 출처
- [Kotlin](https://kotlinlang.org/)
- [Hyperskill: Introduction to Kotlin](https://hyperskill.org/courses/69-introduction-to-kotlin)
- [Kotlin Docs](https://kotlinlang.org/docs/home.html)

---
title: "[Introduction to Kotlin] TODO: Write title"
date: 2024-12-27 10:00:00 +0900
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

TODO: 지난 1회차 공부했던 내용 recap

- - -
## What is a Variable
- 변수는 값을 저장하는 곳으로 문자열, 숫자 등의 것들이 될 수 있다.
- 모든 변수는 다른 변수와 구별하기 위한 이름(식별자, identifier)가 있다.
- 변수의 이름으로 값에 접근할 수 있다.
- 변수는 프로그램에서 자주 사용되는 요소 중 하나로 변수의 사용법을 이해하는 것이 중요하다.

### Declaring variable(in kotlin)
- Kotlin에서는 변수를 선언하기 위해 두 가지 키워드가 존재한다.
- 변수를 선언할 때는 일반적으로 `val`과 `var` 키워드를 사용한다.

1. val(value)
   - `val`은 읽기 전용(read only) 변수로 명명된 값(named value)을 선언한다.
   - 이 변수는 초기화된 후 변경이 불가능하여, **한 번만 값을 할당할 수 있다**.
     > 무조건적으로 한 번만 할당할 수 있는 것은 아니다.

2. var(variable)
   - 필요한 만큼 변경가능한(mutable) 변수를 선언한다.

3. const(constant) val
  - `const val`은 컴파일 시점에 확정되는 값으로 변수를 선언할 때, 초기값이 지정되어야한다. 
    - 예시
      ```kotlin
      const val PI = 3.14159  // 컴파일 시점에 값이 결정됨.
      val PI = 3.14159 // 동일하게 가능함.
      ```
    
      ```kotlin
      val currentTime = System.currentTimeMillis() // 코드가 실행되고 변수 선언 시점이 되면 값이 결정됨.
      const val  currentTime = System.currentTimeMillis() // 컴파일 오류를 일으킴.
      ```
  > 상세한 내용은 다음 [출처](https://itstory1592.tistory.com/104) 참고 바랍니다.

4. `var`과 `val`의 사용 예시
    ```kotlin
    // val 사용 예시
    val language = "Kotlin"
    println(language)
    // 출력 결과: Kotlin
    
    language = "Python" // val은 변경 불가능함.
    // 오류 발생
    // Val cannot be reassigned
    ```
   - val 추가 예
    ```kotlin
    // val 사용 예시
    val boolFalse: Boolean
    println(boolFalse) // 불린이 할당되기 전에 사용되었기에 에러 발생
    ```
    ```kotlin
    // val 사용 예시
    val boolFalse: Boolean
    boolFalse = false // 값 초기화
    println(boolFalse) // 에러 발생하지 않음.
    ```

    ```kotlin
    // var 사용 예시
    var language = "Kotlin"
    println(language)
    // 출력 결과: Kotlin
    
    language = "Python" // var은 변경가능한 변수임.
    println(language)
    // 출력 결과: Python
    language = 10 // var은 초기 값과 동일한 유형의 값으로만 변경 가능함.
    // ERROR: The integer literal does not conform to the expected type String
    ```

- 주의사항
  - 변수 이름은 숫자로 시작할 수 없다.
  - 변수 이름은 의미있고, 이해하기 쉬우며, 읽기 쉬운 이름을 선택해야한다.
    - 변수가 복잡한 역할을 하여 이름을 설정하는 것의 어려움이 있다면 변수 이름이 길어지더라도 작성하는 것이 좋다.
  - 많은 경우 불변 변수(`val`)으로 변수를 선언하는 것이 더욱 좋다.
    - 코드에 가변 변수가 많을수록 코드를 읽고 이해하는 것이 어렵다.

#### Val 변수와 가변성(mutable)
- `val`은 불가변성(immutable)의 동의어가 아니다.
- `val`으로 선언하였더라도 변경 가능한 예외적인 경우가 있다.
- 예시
```kotlin
// mutable list 생성
val mutableList = mutableListOf(1, 2, 3, 4, 5)
// mutable list 변경 요청
mutableList = mutableListOf(1, 2, 3, 4, 5, 6) // 에러 발생
```
- 변수를 재 할당하려면 에러가 발생하나, 내부 상태의 변경은 가능하다.
```kotlin
// mutable list 생성
val mutableList = mutableListOf(1, 2, 3, 4, 5)
// 요소 추가
mutableList.add(6)
// 출력
println(mutableList) // [1, 2, 3, 4, 5, 6]
```
> Java에 익숙하다면, `val`은 Java의 `final`변수와 동일하게 취급하면 된다.  
> 이 둘은 매우 유사한데, 모두 변수에 값을 다시 할당하는 것은 금지하지만 객체의 내부 상태는 변경할 수 있다.


## Const(Constant) 변수
- Kotlin에는 `val` 키워드 앞에 컴파일 타임 상수(`const`)를 선언하는 수정자도 있다.
- 변수의 값은 컴파일 타임에 결정되며 런타임에는 변경되지 않는다.
```kotlin
const val MY_STRING = "This is a constant string"
```
- 아래 코드는 프로그램 실행 전에는 값을 알 수 없고 상수가 아니므로 오류가 발생한다.
```kotlin
const val MY_STRING = readln() // 에러 발생
```
- 몇 가지 수정자를 사용할 수 있는 제한이 있다.
- 아래 예시 참고
```kotlin
const val CONST_INT = 127
const val CONST_DOUBLE = 3.14
const val CONST_CHAR = 'c'
const val CONST_STRING = "I am constant variable"
const val CONST_ARRAY = arrayOf(1, 2, 3) // error: only primitives and strings are allowed
```
- 또한, `const` 변수는 함수 밖의 최상위 수준에서 선언되어야한다.
  > 런타임과 관계 없는 상수이므로 함수 밖에서 선언하는 것 같다.
```kotlin
const val MY_INT_1 = 1024

fun main() {
  const_val MY_INT_2 = 2048 // error: Modifier 'const' is not applicable to 'local variable'
}
```
## Naming Convention
- Kotlin에서 `val`과 `const`를 선언할 때에는 쉽게 작성가능하고 유지할 수 있는 명명 규칙이 있다. 
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
## 출처
- [Kotlin](https://kotlinlang.org/)
- [Hyperskill: Introduction to Kotlin](https://hyperskill.org/courses/69-introduction-to-kotlin)
- [Kotlin Docs](https://kotlinlang.org/docs/home.html)

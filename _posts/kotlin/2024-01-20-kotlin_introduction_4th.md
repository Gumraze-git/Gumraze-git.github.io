---
title: "[Introduction to Kotlin] 명명 규칙, Java Scanner"
date: 2025-01-20 10:00:00 +0900
layout: post
category: Kotlin
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Naming and Standard Input Streeeeeeam and Scaaaaaaaaner
pin: false
---
- - -
# **시작하면서,,**
이번 게시글은 간단한 명명규칙 그리고 `Java Scanner`를 포함한 여러 출력 방법에 대해 공부한 것을 공유하고자 한다.

- - -
## **Naming Rule**
좋은 프로그래머는 신중하게 변수에 이름을 붙여 코드를 읽고 따라가는데 어려움이 없다.  
따라서 **항상 모든 변수에 설명적이고 간결한 이름을 지정해야한다.**

Kotlin의 **몇 가지 명명규칙**은 아래와 같다.
- 이름은 대소문자를 구분한다.
  >`number`와 `Number`는 다르다.
- 각 이름에는 문자, 숫자, 밑줄만 포함될 수 있다.
- 이름은 키워드가 될 수 없다.
  - ex) `var`, `val`, `fun`
- 공백이 허용되지 않는다.
  - 사실 백틱을 이용하여 가능하다.

  ```kotlin
  val `kotlin value can this` = 5
  ```

- 변수가 한 단어인 경우 소문자로 입력한다.
  - ex) `number`, `value`
- 변수 이름에 여러 단어가 포함되어 있는 경우, 첫 단어는 소문자로 나머지 단어는 대문자로 시작해야한다.
  - ex) `lowerCamelCase`, `numberOfCoins`
- 변수를 밑줄로 시작하지 않는다.
  - 기술적으로는 가능하다.
- 변수에 의미 있는 이름을 선택해야한다.
  - ex) `s`도 가능하지만, `score`라고 작성하는 것이 더 의미가 있다.

### **Magin numbers: 매직 넘버**
코드 작성 중에 상수를 사용해야하는 경우가 있다.  
**예를 들어)** 1주일이 며칠인지 출력해야하는 경우 아래와 같이 작성할 수 있다.
```kotlin
println(7)
```
위 코드는, `7`이 가지는 의미가 어떤 것인지에 대한 단서가 없다.  
코드에서는 이러한 값들을 **매직 넘버(magic number)**라고 한다.

> 매직 넘버는 반드시 숫자가 아니며, 단서가 없는 데이터의 본질을 이야기한다.

따라서 이러한 경우에는 아래와 같이 처리해야한다.

- **불변 변수(immutable variable)인 상수(const)**로 취급한다.  
  
  ```kotlin
  const val DAYS_OF_THE_WEEK = 7
  
  fun main() {
      // ...
      println(DAYS_OF_THE_WEEK)
      // ...
  }
  ```

- 상수의 변수 이름에는 의미가 담기도록 명명한다.
> `SCREAMING_SNAKE_CASE` 스타일을 사용한다.

  ```kotlin
  const val SEASONS = 4 // 스크리밍 스네이크 케이스
  ```

- - -
## **Standard output: 표준 출력**
> 표준 출력은 하드웨어 장치에 정보를 표시하는 기본 작업이다.

### **Printing text: 텍스트 출력**
텍스트 출력 방법은 아래와 같다.
```kotlin
println("Hello, Kotlin") // 큰 따옴표를 이용하여 문자열 출력 가능함.
println(7) // 숫자는 따옴표 없이 출력 가능함.
print("days") // print함수는 줄바꿈 없이 작동함.
println() // 공백으로 줄바꿈 가능함.
println("Kotlin!")
```
**실행 결과**
```text
Hello, Kotlin
7days
            // 공백
Kotlin!
```

### **String formatting: 문자열 포매팅**
문자열 포매팅은 출력함수에 변수를 삽입하는 방법으로 다양한 방법으로 문자열 포매팅이 가능하다.  
일반적으로 **Kotlin에서 `$` 연산자는 문자열 템플릿에서 변수나 표현식의 값을 문자열에 직접 삽입**하는데 자주 사용된다.  
사용 예시는 아래와 같다.

1. 변수 값 삽입.
```kotlin
val name = "Kotlin"
println("Hello, $name!") // 출력: Hello, Kotlin!
```
2. 표현식 삽입
```kotlin
val a = 5
val b = 10
println("Sum of $a and $b is ${a + b}") // 출력: Sum of 5 and 10 is 15
```
3. Kotlin에서 `$`를 출력하는 방법
`$`뒤에 `.`이 오면 문제 없이 출력된다.
```kotlin
val a = 20
println("The price is $a$.") // 출력: The price is 20$.
```

4. Java의 `String.format` 메서드 이용
```kotlin
val name = "Alice"
val age = 25
println(String.format("My name is %s and I am %d years old.", name, age))
// 출력: My name is Alice and I am 25 years old.
```

## **Invoking functions: 함수 호출**
함수는 일련의 명령어이며, 이름을 호출하여 프로그램에서 호출 할 수 있다.
기본적으로, 그것은 입력 인수(input)을 처리하고 유용한 결과를 생성한다.

### **Functions arguments: 함수 인수**
함수를 사용하고 싶을 때, 함수 이름뒤에 괄호를 붙여 호출할 수 있다.
함수가 하나 이상의 인수를 취하는 경우, 괄호 안에 값을 전달해야한다.

아래 예시 `println`는 단일 문자열 인수로 함수를 호출한다.
```kotlin
val text = "Hello, Kotlin"
println(text)
```

`println`은 새로운 줄을 출력하기 위해 인수를 전달하지 않아도 가능하다.
```kotlin
println()
```

### **Producing a result**
일부 함수는 인수를 받을 뿐만 아니라 결과를 생성(반환)하기도 한다.
```kotlin
val result = function(arg)
```
이는 일반 수학 함수와 동일하게 작동한다.

예를 들어, 숫자에 절대값을 반환하는 수학 함수는 아래와 같다.
```kotlin
val number = -10
val nonNegNumber = Math.abs(number) // 10
```

함수를 사용하는 이점은 아무것도 구현할 필요없이, 함수를 호출하기만 하면 작동한다는 것이다.
> 여기서의 함수는 이미 작성된 함수를 이야기한다.

`abs` 함수의 이름은 점(.) 기호 뒤에 작성된다. 그 이유는 `Math`가 여러 함수를 그룹으로 묶어 두었기 때문이며, 특정 함수를 호출하려면 그룹 이름(Math)을 함께 작성해야한다.

모든 함수는 결과를 반환한다. 심지어 `println`의 함수도 결과를 반환한다.
```kotlin
val result = println("text")
println(result) // kotlin.Unit
```

위 함수의 결과로 `kotlin.Unit`을 반환하는데, **`Unit`은 실제로는 "결과 없음"을 의미한다.**
> 함수가 아무것도 반환하지 않을 때, 사실은 Unit을 반환한다.

- - -
## **Standard input with Java Scanner**
표준 입력에서 데이터를 읽기 위해 `readin()`만 사용하는 것이 충분하지 않을 때가 있다.
> `readin()`은 간단한 메서드로 복잡한 작업에는 적합하지 않다.
> 예를 들어 데이터 흐름에서 정수만 찾거나, 데이터를 순차적으로 한 단어씩 읽기 등,,

이 섹션은 Kotlin에서도 사용할 수 있는 **Java 도구인 Scanner를 사용하는 방법을 공유**한다.

### **Java Scanner란?**
Scanner는 표준 입력에서 데이터를 얻는 또 다른 방법이다.  
Kotlin은 Java 라이브러리와 상호 운용이 가능하므로 Scanner를 직접 사용할 수 있다.  
Scanner는 프로그램이 문자열, 숫자 등 다양한 유형의 값을 표준 입력에서 읽을 수 있도록 한다.  

**Java Scanner를 사용하기 위해서는 파일 소스 코드 상단에 `import`문을 추가해야한다.**
```kotlin
import java.util.Scanner
```

그 다음 변수를 다음과 같이 초기화해야한다.
```kotlin
val scanner = Scanner(System.`in`)
```

> 위 코드에서 **System.`in`**은 표준 입력 스트림(Standard input stream)을 나타내는 객체이다.  
> Scanner는 내부 데이터 소스로 감싸고 작업하기 편리한 여러 메서드를 제공한다.

- Scanner를 사용하면 아래와 같은 것을 사용 가능하다.  
아래와 같은 입력값이 주어졌을 때,
```text
Hello, Kotlin
Hello, Kotlin 123
Hello, Kotlin 123
```
```kotlin
val line = scanner.nextLine() // 전체 입력값 반환, 예: "Hello, Kotlin"
val num = scanner.nextInt()   // 숫자 읽기, 예: 123
val string = scanner.next()   // 단어 읽기, 예: "Hello"
```
> `scanner.next()`는 한 단어만 읽으며 줄 전체를 읽지 않는 메서드이다.  
> ex) input: `Hello, Kotlin`/ output: `Hello`

  > 자세한 내용은 [Class Scanner 문서 참조](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html).  
 
#### **예시 프로그램**
아래 프로그램은 두 숫자를 읽고, 순서를 뒤집어 두 개의 다른 줄에 출력하는 프로그램이다.
```kotlin
import java.util.Scanner // Java 표준 라이브러리 클래스

fun main() {
    val scanner = Scanner(System.`in`) // 데이터 읽기

    val num1 = scanner.nextInt() // 첫 번째 숫자 읽기
    val num2 = scanner.nextInt() // 두 번째 숫자 읽기

    println(num2) // 두 번째 숫자 출력
    println(num1) // 첫 번째 숫자 출력
  
    scanner.close() 
}
```

> 데이터를 읽은 후 더 이상 Scanner가 필요하지 않다면, `close()` 메서드를 사용하여 Scanner를 닫아야 한다.  
> Scanner는 지속적으로 PC의 리소스를 사용한다.

#### **사용자 정의 구분자(custom delimiter)**
Scanner는 공백이나 줄바꿈 외의 구분자로 데이터를 읽을 수 있다.
```kotlin
val scanner = Scanner("123_456")
```

공백이나 줄바꿈이 없는 경우, `useDelimiter()` 메서드를 사용하여 구분자를 지정할 수 있다.
예시로 `_`를 구분자로 설정하기 위해서는 아래와 같이 가능하다.
```kotlin
scanner.useDelimiter("_")
```

이제 데이터를 개별적으로 읽을 수 있다.
```kotlin
println(scanner.nextInt()) /// 123 출력
println(scanner.nextInt()) /// 456 출력
```

#### **다음 요소 확인하기**
`Scanner`로 데이터를 읽을 때, 읽을 데이터가 남아 있는지 확인하기 위해서는 `hasNext()`를 사용 가능하다.
```kotlin
val scanner = Scanner("Hello, Kotlin!")
```
위 코드에서 데이터를 아래와 같이 읽을 수 있다.
```kotlin
val word1 = scanner.next() // Hello,
val word2 = scanner.next() // Kotlin!
```

그런데 존재하지 않는 세 번째 단어를 읽으려고 하면 예외가 발생하여 프로그램이 중단된다.  
이를 방지하기 위해 `hasNext()`를 사용 가능하다.

```kotlin
if (scanner.hasNext()) val word1 = scanner.next() // Hello,
if (scanner.hasNext()) val word2 = scanner.next() // Kotlin!
if (scanner.hasNext()) val word3 = scanner.next() // 읽을 데이터가 없으므로 실행되지 않음
```

# **마치며,,**
프로그램을 테스트 할 때, Java Scanner를 이용하면 테스트에 더욱 용이 할 수 있을 것 같다.

---
title: "[Introduction to Kotlin] 문자열 및 연산자"
date: 2025-02-05 10:00:00 +0900
layout: post
category: Kotlin
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description:  String and Operator
pin:
---
- - -
## **String basics: 문자열의 기본**
Kotlin에는 String, Int, Double과 같은 많은 데이터 타입이 있다.
오늘은 `String`에 대해 다뤄보고자 한다.  
`String`은 큰 따옴표("")로 묶인 0개 이상의 문자로 이루어진 시퀀스이다.
오늘 주제에서는 문자열을 다루는데 중요한 기본 사항들을 살펴본다.

### **The length of a string**
문자열의 길이는 `.length`를 이용하여 계산할 수 있으며, `Int` 타입의 값을 반환한다.
```kotlin
val language = "Kotlin"
println(language.length) // 출력: 6
```

### Concatenating strings: 문자열 연결
Kotlin에서는 `String`도 일반적인 연산이 가능하다.
```kotlin
val str1 = "ab"
val str2 = "cde"
val result = str1 + str2 // 출력: "abcde"
```

아래와 같은 연산도 가능하다.
```kotlin
val firstName = "First"
val lastName = "Last"
val fullName = firstName + "Middle" + lastName // 출력: FirstMiddleLast
```

### Appending values to strings: 문자열에 값 추가하기
`+` 연산자는 다른 타입의 값을 문자열에 추가할 때도 사용할 수 있다.  
값은 자동으로 문자열로 변환된 후 대상 문자열에 연결된다.

```kotlin
val stringPlusBoolean = "abc" + 10 + true
println(stringPlusBoolean) // abc10true

val code = "123" + 456 + "789"
println(code) // 123456789
```
그러나, 첫 번째 피연산자가 숫자인 경우 에러가 발생한다.
```kotlin
val errorString = 10 + "abc" // Error 발생
```

또한, 문자(character)를 문자열과 연결하면 새로운 문자열을 생성할 수 있다.
```kotlin
val charPlusString = 'a' + "bc"
println(charPlusString) // abc

val stringPlusChar = "de" + 'f'
println(stringPlusChar) // def
```
### Repeating the string: 문자열 반복하기
하나의 문자열을 두 번 이상 반복해야하는 경우, 반복문을 사용할 필요가 없다.  
`.repeat(x)`함수를 이용하여 반복 가능하다.
```kotlin
println("Hello".repeat(4)) // HelloHelloHelloHello 
```

### **Raw string**
가끔 문자열에 탭 또는 따옴표 등의 특수 기호가 필요할 때가 있다.  
이러한 경우에는 이스케이프 시퀀스(escape sequence)를 이용하여 사용할 수 있다.
```kotlin
println("\'H\' is the first letter of \"Hello world!\" string.")
// 'H' is the first letter of "Hello world!" 문자열 출력
```
위 방식은 간단한 문자열에는 유용하지만, 긴 텍스트를 작성할 때는 가독성이 떨어질 수 있다.
이러한 경우에는 **`Raw string`**을 사용 가능하다.  
`Raw string`은 삼중 따옴표로 감싸서 사용한다.
```kotlin
val largeString = """
    This is the house that Jack built.
      
    This is the malt that lay in the house that Jack built.
       
    This is the rat that ate the malt
    That lay in the house that Jack built.
       
    This is the cat
    That killed the rat that ate the malt
    That lay in the house that Jack built.
""".trimIndent() // 공백 줄과 공통 들여쓰기를 제거합니다.
print(largeString)
```
**출력 결과**
```text
This is the house that Jack built.

This is the malt that lay in the house that Jack built.

This is the rat that ate the malt
That lay in the house that Jack built.

This is the cat
That killed the rat that ate the malt
That lay in the house that Jack built.
```
> `.trimIndent()`는 공통 최소 들여쓰기를 잘라내고, 첫 번째 및 마지막 줄이 비어 있다면 이를 제거합니다.  

- - -
## **Boolean type and operations(True and false): 불리언 타입과 연산**
### **Boolean variables: 불리언 변수**
불리언은 `true`와 `false` 두 가지 값만 가질 수 있는 데이터 타입이다.
```kotlin
val t = true
val f = false
```
### **Reading boolean values: 불리언 값 읽기**
Kotlin 1.6 이상부터는 아래와 같이 불리언 값을 읽을 수 있다.
```kotlin
val b: Boolean = readln().toBoolean()
```
`toBoolean()`은 입력값이 대소문자를 구분하지 않고 `true`인 경우에 `true`를 반환한다.

```text
true  -> true
True  -> true
TrUe  -> true
trUE  -> true
T     -> false
Truth -> false
```

### **Logical operators: 논리 연산자**
불리언 타입의 변수는 논리 연산자를 사용하여 논리적인 문장을 구성할 수 있다.
Kotlin에는 4가지 논리 연산자가 있다.
- **NOT 연산자**
  - NOT 연산자는 단항 연산자로 불리언 값을 반전시킨다.
  ```kotlin
  val f = false
  val t = !f
  ```
- **AND 연산자**
  - AND 연산자는 이항 연산자로, 두 피 연산자가 모두 `true`일 경우 `false`를 반환한다.
  ```kotlin
  val b1 = false && false // false
  val b2 = false && true // false
  val b3 = true && true // false
  val b4 = true && true // true
  ```
- **OR 연산자**
  - OR 연산자는, 적어도 하나의 피연산자가 `true`인 경우에 `true`를 반환한다.
  ```kotlin
  val b1 = false || false // false
  val b2 = false || true // true
  val b3 = true || false // true
  val b4 = true || true // true
  ```
- **XOR 연산자**
  - XOR(exclusive OR) 연산자는 이항 연산자로, 불리언 피연산자가 서로 다른 값을 가질 경우 true를 반환한다.
  ```kotlin
  val b1 = false xor false // false
  val b2 = false xor true  // true
  val b3 = true xor false  // true
  val b4 = true xor true   // false
  ```

### **Logical operator preceduence: 논리 연산자의 우선순위**
일반적으로 그렇듯이 Kotlin에도 논리 연산의 우선 순위가 있다.
1. NOT(!)
2. XOR(xor)
3. AND(&&)
4. OR(||)

아래 예시를 확인해보자.
```kotlin
val bool = true && !false // -> true, NOT 먼저 연산 후 AND를 연산하기 때문.
```

논리 연산의 순서를 결정하고 싶다면, 일반적인 수학 규칙과 동일하게 괄호`()`를 이용하면 된다.

- - -
## **Arithmetic operations: 산술 연산자** 
Kotlin에는 일반적인 다섯 가지의 산술 연산자가 있다.
- Addition: `+`
- Subtraction: `-`
- Multiplication: `*`
- Integer division(정수 나눗셈): `/`
- Modulus(모듈러수, 나머지 연산): `%`

위 연산자들은 이항 연산자로 두 개의 값을 피연산자로 사용한다.
사용 예시는 아래와 같다.
```kotlin
println(10 + 10) // 20
println(10 - 10) // 0
println(10 * 10) // 100
println(12 / 10) // 1
println(12 % 10) // 2
```

> 음수의 나눗셈은 다르게 동작한다.  
> 추후 다루도록 함.

### **Unary operator: 단항 연산자**
단항 연산자는 하나의 값을 피연산자로 취급한다.
```kotlin
println(+5) // 5
println(+(-5)) // -5
println(-8) // -8
```
> 단항 덧셈 및 뺄쎔 연산자는 곱셈 및 나눗셈 연산자보다 높은 우선순위를 가진다.

### **Precedence order: 우선순위 순서**
아래는 산술 연산자의 우선순위 목록이다.

1. 괄호, `()`
2. 단항 덧셈/뺄셈, `+`/`-`
3. 곱셉, 나눗셈, 나머지
4. 덧셈 및 뺄셈

## **Increment and decrement: 증가 및 감소 연산**
### **Assignment operations: 할당 연산**
Kotlin에서는 기본적인 산술 연산(덧셈, 뺄셈 등)을 지원한다.
```kotlin
var a = 3
a = a + 1 // 4
a = a - 1 // 3
```

또한, Kotlin에서는 산술 연산과 할당을 결합한 복합 할당 연산(compound assignment operation)이 가능하다.  
이를 사용하면 변수를 2번 반복하지 않고 간단히 표현할 수 있다.
```kotlin
var a = 3
a += 2 // 5
a -= 2 // 3
a *= 2 // 6
a /= 2 // 3
a %= 2 // 1
```

### **Using Increment and decrement: 증가 및 감소 사용하기**
숫자를 1씩 증가시키거나 감소시키는 작업은 자주 사용하는 작업 중 하나이다.  
물론, `a += 1` 또는 `a -= 1`을 사용할 수 있지만, Kotlin은 이를 더 간단하게 처리할 수 있는 연산자를 제공한다.
```kotlin
var num = 3
num ++ // 4, 증가
num -- // 3, 감소
```
> 위 연산자들은 숫자를 1씩 증가시키거나 감소시킬 때문 사용할 수 있다.

증가 및 감소 연산자는 전위(prefix)와 후위(postfix) 연산자를 알면 더욱 복잡한 연산도 가능하다.

### **Prefix form: 전위 형태**
전위 형태는 **변수를 사용하기 전에 값을 변경**하는 특성을 가지고 있다.

- 전위 증가(prefix increment)
```kotlin
var a = 10
val b = ++a
println(a) // a = 11
println(b) // b = 11
```
위의 코드에서는 먼저 변수 `a`의 값이 `1` 증가하여 `11`이 된 후, 증가된 값이 변수 `b`에 할당된다.

- 전위 감소(prefix decrement)
```kotlin
var a = 10
val b = --a
println(a) // a = 9
println(b) // b = 9
```
위 코드에서도 마찬가지로 변수 `a` 값이 `1` 감소한 뒤, 변수 `b`에 할당된다.

### **Postfix form: 후위 형태**
후위 형태는 **변수를 사용 한 후에 값을 변경**하는 특성을 가지고 있다.

- 후위 증가(postfix increment)
```kotlin
var a = 10
val b = a++
println(a) // a = 11
println(b) // b = 10
```
위의 코드에서 변수 `a`의 현재 값 `10`이 변수 `b`에 할당된다.
그 후, `a`의 값이 `1` 증가하여 `11`이 된다.

- 후위 감소(postfix decrement)
```kotlin
var a = 10
val b = a--
println(a) // 9
println(b) // 10
```
마찬가지로 변수가 `a`는 변수 `b`에 할당 된 후, 감소를 수행한다.

### **Order of precedence: 우선순위 순서**
위 다루었던 연산들과 최종적으로 전위 및 후위 형태의 연산자를 포함한 연산 우선순위의 순서는 아래와 같다.

1. 괄호( (expr) )
2. 후위 증가/감소( expr++, expr-- )
3. 단항 덧셈/뺄셈 및 전위 증가/감소( -expr, ++expr, --expr )
4. 곱셈, 나눗셈, 나머지( *, /, % )
5. 덧셈/ 뺄셈( +, -)
6. 할당 연산( =, +=, -=, *=, /=, %= )









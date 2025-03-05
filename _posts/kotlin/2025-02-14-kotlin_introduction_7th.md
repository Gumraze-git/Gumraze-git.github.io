---
title: "[Introduction to Kotlin] Kotlin의 기본 타입과 타입 변환"
date: 2025-02-14 10:00:00 +0900
layout: post
category: [Kotlin]
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Type can be conversion but you may have to be careful.
pin: false
---

- - -

## **기본 타입의 속성**

이 주제에서는 Kotlin의 기본 타입을 분류하고 각 속성에 대해 알아본다.
기본 타입은 의미에 따라 여러 그룹으로 나울 수 있으며, 같은 그룹 내 타입들은 유사하게 동작하지만 크기가 다르므로 표현할 수 있는 값의 범위도 다르다.

## **숫자**

Kotlin은 정수(int) 및 실수(float)를 표현하는 여러 숫자(numbers) 타입을 제공한다.

### **정수 타입**

정수(integer)는 다음 4가지 타입으로 표현된다.
이들은 크기가 다르며, 표현할 수 있는 값의 범위도 다르다.

| 타입    | 크기         | 범위                                                |     |
|-------|------------|---------------------------------------------------|-----|
| Byte  | 8비트(1바이트)  | -128                                              | 127 |
| Short | 16비트(2바이트) | -32,768                              | 32,767          |
| Int   | 32비트(4바이트) | -2,147,483,648                       |  2,147,483,647   |
| Long  | 64비트(8바이트) | --9,223,372,036,854,775,808   | 9,223,372,036,854,775,807    |

정수 타입의 범위는 $-(2^n - 1) \sim (2^n - 1) - 1$ 수식으로 계산된다.

> 여기서 $n$은 비트(bit)수이다.  
> 0이 범위에 포함되므로 최댓값에서 1을 빼준다.

가장 일반적으로 사용되는 정수 타입은 `Int`와 `Long`이다.  
가능하면 `Int`를 사용하고, 더 큰 숫자가 필요할 경우 `Long`을 사용하면 된다.  

```kotlin
val zero = 0 // Int
val one = 1  // Int
val oneMillion = 1_000_000  // Int

val twoMillion = 2_000_000L           // Long (L을 붙여서 명시)
val bigNumber = 1_000_000_000_000_000 // Long (Int의 범위를 넘어, 표현할 수 없어서 자동으로 Long 타입으로 변환됨)
val ten: Long = 10                    // Long (명시적으로 타입 지정)

val shortNumber: Short = 15 // Short (명시적으로 타입 지정)
val byteNumber: Byte = 15   // Byte (명시적으로 타입 지정)
```

### **실수 타입**
실수(float)를 표현하는 타입은 2가지가 있다.

|타입| 크기         | 정밀도 |
| -- |------------|-----|
| Float| 4바이트(32비트) | 약 6~7자리 정밀도 |
| Double | 8바이트(64비트)   | 약 14~16자리 정밀도|

`Float`과 `Double`은 소수점을 포함한 숫자를 저장할 수 있지만, 저장할 수 있는 자릿수에 제한이 있다.

> 실무에서는 `Double`이 더 일반적으로 사용된다.
> 정밀도(precision): 실제 정답이라고 예측한 것들 중에 실제 정답의 비율
> 정확도(accuracy): 전쳬 예측 중 올바르게 예측한 비율

```kotlin
val pi = 3.1415              // Double
val e = 2.71828f             // Float (f를 붙여서 명시)
val fraction: Float = 1.51f  // Float (명시적으로 타입 지정)
```

### **숫자 타입의 최소/최대값**
숫자 타입의 최소값과 최대값을 출력하려면 타입 이름 뒤에 `.MIN_VALUE` 또는 `.MAX_VALUE`를 붙이면 된다.
```kotlin
println(Int.MIN_VALUE)  // -2147483648
println(Int.MAX_VALUE)  // 2147483647
println(Long.MIN_VALUE) // -9223372036854775808
println(Long.MAX_VALUE) // 9223372036854775807
```

또한, 타입의 크기를 바이트 또는 비트 단위로도 확인할 수 있다.
> 1byte = 8bit

```kotlin
println(Int.SIZE_BYTES) // 4 (바이트)
println(Int.SIZE_BITS)  // 32 (비트)
```

## **문자**
Kotlin 에서는 문자(characters)를 표현하기 위해 `Char` 타입을 사용한다.  
영어 대소문자, 숫자, 기타 기호를 표현할 수 있으며 싱글 쿼트(`''`)로 감싼다.  
`Char` 타입의 크기는 `Short` 타입과 동일하게 2바이트(16비트)이다.

```kotlin
val lowerCaseLetter = 'a'
val upperCaseLetter = 'Q'
val number = '1'
val space = ' '
val dollar = '$'
```

> `Char` 타입은 여러 언어의 문자(ex: 한자, 특수 문자 등)도 표현할 수 있다.

## **불리언**
Kotlin에는 불리언(boolean) 타입이 있으며, 참(true) 또는 거짓(false) 2가지 값만 저장할 수 있다.  
이론적으로는 1비트만 필요하지만, 실제 크기는 정확히 정의되지 않았다.

> 실제 크기가 정확히 정의되지 않은 이유는 JVM(Java Virtual Machine)의 최적화 방식 및 메모리 정렬 방식 때문임.
> 추후 JVM에 대해 다루면서 같이 찾아볼 예정임.

```kotlin
val enabled = true
val bugFound = false
```

## **문자열**
문자열(string) 타입은 연속된 문자들을 표현하며, 큰 따옴표(`""`)로 감싼다.  
> Kotlin에서 가장 많이 사용되는 타입 중 하나이다.

```kotlin
val creditCardNumber = "1234 5678 9012 3456"
val message = "Learn Kotlin instead of Java."
```

- - -
## **타입 변환하기**
**타입 변환(type conversion)** 또는 **타입 캐스팅(type casting)**은 한 데이터 타입의 값을 다른 데이터 타입으로 변경하는 과정이다.
타입을 지정하고 변환하는 작업은 특히 Kotlin에서 중요한데, **Kotlin은 정적 타입 언어(statically typed language)**이기 때문이다.

### **숫자 타입 간의 변환**
Kotlin에서 가장 일반적으로 사용되는 숫자(numeric) 타입은 `Int`, `Long`, `Double`이다.

> 위 타입을 변경하기 위해 `toInt()`, `toLong()`, `toDouble()`이 사용 가능하다.  

숫자 타입을 적절하게 사용하지 않으면 **타입 불일치(type mismatch)** 오류가 발생하게 된다.

```kotlin
import kotlin.math.sqrt

val num: Int = 100
val res: Double = sqrt(num.toDouble())
// 위 코드에서 제곱근을 구하기 위해 toDouble() 타입을 변경하지 않으면 타입 불일치 오류가 발생한다.
```

#### **Char 타입 변환**
`Char`은 단일 문자를 작성할 때 사용되는 타입이다.
그런데, Kotlin에서는 숫자를 `toChar()`으로 상호변환이 가능하다.

```kotlin
val number: Int = 125
val char: Char = num.toChar() // }
val charToNumber: Int = char.code() // 125
```

Kotlin에서는 정수(Int)를 문자(Char)로 변환 시, 이에 대응되는 문자의 유니코드(unicode) 값으로 변환된다.

### **Short 및 Byte 타입 변환**
Short 및 Byte 타입은 매우 작은 숫자 범위를 가지므로 비교적 잘 사용되지는 않는다.
일반적으로 정수를 사용하기 위해서는 `Int` 타입을 사용하는 것이 적절하다.

> `Double` 또는 `Float` 타입을 `Short` 또는 `Byte`로 직접 변환하면 변수의 크기가 너무 작아 예상치 않은 결과가 발생할 수 있다.  
> 따라서, Kotlin 1.4 부터는 `Double` 또는 `Float` 타입을 `Short` 또는 `Byte`로 직접 변환하지 못하도록 수정 되었다.

### **문자열 변환**
종종 다른 타입의 값을 문자열(string)로 변환해야하는 경우가 있다.  
Kotlin에서는 `toString()`을 이용하여 어떤 타입의 값이든 문자열로 변환 할 수 있다.

```kotlin
val num = 8
val double = 10.09
val char = '@'
val bool = true

val numToStr = num.toString()
val doubleToStr = double.toString()
val charToStr = char.toString()
val boolToStr = bool.toString()
```

반대로 숫자 및 불리언을 문자열로 변환 할 수 있다.
```kotlin
val num = "10".toInt()
val doub = "10.25".toDouble()
val bool = "true".toBoolean()
```

> 만일, 문자열을 불리언으로 변환할 경우에는 불리언이 적절하게 작성되지 않아도 오류가 발생하지 않는다.  
> 반면에, **숫자가 아닌 문자열을 숫자로 변환할 경우에는 오류가 발생하여 프로그램이 중단**된다.

### **타입 변환 시 문제점**
큰 숫자를 작은 타입으로 변경할 경우 값이 손실되게 된다.

```kotlin
val double: Double = 12.5
val number = double.toInt() // 12

val veryBigBigNumber: Long = 100_000_000_000_000
val n = veryBigBigNumber.toInt() // 276_447_232, 정수가 가질 수 있는 최대값
```
> 큰 값을 작은 타입으로 변환할 경우 값이 소실되는 것을 **타입 오버플로우(type overflow)**라고 한다.  
> 따라서, 값을 변환할 때 데이터의 손실 여부를 고려해야한다.


- - -
## **타입 강제 변환: 서로 다른 타입이 만날 때**
위의 설명으로 `Int` 타입의 변수를 `Long`변수에 직접 할당 할 수 없다는 것을 알게 되었다.  
하지만, `Int`와 `Long` 변수의 덧셈을 하면 일어날까?  
이러한 경우에는 문맥(context)에서 타입이 추론(infer)된다.

### **타입 강제 변환**
이러한 상황에서는 컴파일러가 자동으로 모든 구성 요소를 설정하는 타입 강제 변환(type coericion)이 일어난다.  
이 경우 결과의 타입을 표현식에서 가장 넓은(widest) 타입으로 설정한다.  
아래 그림은 이러한 타입 캐스팅(casting)의 방향을 나타낸다. 

![type_coercion_direction.png](/assets/attachment/kotlin_study/type_coercion_direction.png)

> 결과 타입이 이전 타입보다 더 넓기 때문에 정보 손실이 발생하지 않는다.  
> 또한, 이는 숫자 타입과 문자열 타입에서만 작동한다.

#### **예제**
- `Int`에서 `Long`으로 변환
  ```kotlin
  val num: Int = 100
  val longNum: Long = 1000
  val result = num + longNum // 1100, Long으로 변환됨.
  ```

- `Long`에서 `Double`로 변환
  ```kotlin
  val bigNum: Long = 1000000
  val doubleNum: Double = 0.0
  val result = bigNum - doubleNum // 1000000, Double으로 반환됨.
  ```

- `Short`와 `Byte`의 변환
  - `Short`와 `Byte`는 예외적인 특징을 가지고 있다.  
  - 이 타입들로 연산을 수행하면 항상 `Int`를 반환한다.

  ```kotlin
  // Byte + Byte = Int
  val one: Byte = 1
  val two: Byte = 2
  val three = one + two // 3, Int
  ```
  
  ```kotlin
  // Short + Short = Int
  val fourteen: Short = 14
  val ten: Short = 10
  val four = fourteen - ten // 4, Int
  ```

- - -
## 부호 없는 정수
기본적으로 Kotlin의 모든 정수 타입은 양수와 음수를 모두 저장할 수 있다.  
하지만, 부호 없는 정수(Unsigned Integers)도 지원한다.  
이러한 경우의 정수는 음수를 저장할 수 없으며, 0이상의 값만 저장할 수 있다.  

|타입|설명|범위|
|---|---|---|
|UByte| 8비트 부호 없는 정수| 0 ~ 255|
|UShort | 16비트 부호 없는 정수| 0 ~ 65,535|
|UInt | 32비트 부호 없는 정수 | 0 ~ 4,294,967,295|
|ULong | 64비트 부호 없는 정수 | 0 ~ 18,446,744,073,709,551,615|

부호 없는 정수는 일반 정수처럼 생성할 수 있으며, `u` 또는 `U` 접미사를 붙여야한다.  

```kotlin
val unsignedByteType: UByte = 5u
val unsignedTypeShort: UShort = 10u
```

타입을 명시하지 않으면, 크기에 따라 타입이 결정되며, 특수 접미사 `uL` 또는 `UL`을 사용하면 무조건 `ULong`이 된다.

```kotlin
val smallSize = 100u // UInt 타입으로 지정됨.
val bigSize = 5_000_000_000u // ULong 타입으로 지정됨.
val smallLong = 10uL // 특수 접미사 `uL` 사용으로 `ULong`으로 지정됨.
```

- - -
## 데이터 타입 오버플로우
모든 정수 타입은 특정 범위를 초과하면 오버플로우(overflow)가 발생할 수 있다.  

아래 예제를 살펴보면,
```kotlin
// Int의 최대값: 2_147_483_647
var d: Int = 2_146_482_647
d += 1
println(d) // -2_147_483_648
```

변수 `d`가 `Int`의 최댓값(2,147,483,647)을 초과하여 오버플로우가 발생했다.  
따라서 변수의 값이 `Int`의 최솟값(-2,147,483,648)으로 변환되었다.  
이와 같은 현상을 **데이터 타입 오버플로우(data type overflow)**라고 한다.

### 오버플로우의 원리
컴퓨터는 2진수(0과 1)로 숫자를 저장한다.
`Int`의 경우에는 **최상위 1비트(MSB, Most Significant Bit)는 부호(sign) 비트로 사용**되며,
나머지 **31비트는 실제 숫자를 표현하는데 사용**된다.

```text
2_147_483_647 = 01111111111111111111111111111111
```
위 비트에서 1을 더하면 아래와 같이 왼쪽 비트가 1로 바뀌면서 음수로 변환된다.
```text
10000000000000000000000000000000 = -2_147_483_648
```

![data_overflow.webp](/assets/attachment/kotlin_study/data_overflow.webp)

따라서, 데이터 타입 오버플로우가 발생하면 데이터의 손실이 일어나 예측할 수 없는 값이 나올 수 있다.
> 데이터 타입 오버플로우는 프로그래머의 실수이므로 주의가 필요하다.

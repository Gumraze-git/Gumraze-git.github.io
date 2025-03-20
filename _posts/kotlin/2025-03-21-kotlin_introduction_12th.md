---
title: "[Introduction to Kotlin] 반복문 (repeat, while, do while)"
date: 2025-03-21 10:00:00 +0900
layout: post
category: [Kotlin]
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Again and again and again and again and
pin: false
---
- - -

## **반복문**

때떄로 특정 코드 블록을 여러 번 실행해야 할 떄가 있다.  
이때 단순하게 복사 & 붙여넣기로 코드를 반복 실행할 수 있겠지만, 만약 10만 번 반복해야하는 경우라면?

**복사 & 붙여넣기는 비효율적이다.**

Kotlin은 코드 블록을 반복 실행할 수 있는 문법인 반복문을 제공한다.

### **Repeat**
가장 간단한 반복문인 `repeat(n) { ... }`은 반복할 횟수를 `n`에 넣고 중괄호 안에 실행할 코드를 넣으면 된다.

아래 코드는 `Hello`를 10번 출력한다.
```kotlin
fun main() {
    repeat(10) {
        println("Hello")
    }
}
```
> 만약 `n`이 `0` 이하의 값이면, `repeat` 메서드는 실행되지 않는다.

또한, **`it`을 사용하여 현재 반복 횟수를 확인할 수 있다.**

```kotlin
fun main() {
    repeat(3) { // 람다 표현식 사용
        println(it)
    }
}
```

> **람다 표현식**  
> `{ ... }`안에 있는 코드 블록을 람다 표현식(lambda expression)이라고 한다.  
> 람다는 **이름이 없는 함수**이며, 즉시 실행할 수 있는 익명 함수의 역할을 한다.
{: .prompt-tip }

### **repeat을 사용하여 입력값 처리하기**
반복문 안에서 입력을 읽고, 변수를 선언하고, 연산을 수행할 수 있다.    
다음 프로그램은 **표준 입력에서 숫자를 읽고, 합을 계산**한다.

```kotlin
fun main() {
    val n = readln().toInt() // 반복할 횟수 입력 받음
    var sum = 0
    
    repeat(n) {
        val next = readln().toInt()
        sum += next // n 번 반복하여 수를 합산함
    }
    println(sum)
}
```

- - -
## **While 루프**
Kotlin에는 특정 조건이 참인 경우에 반복하는 여러 방법이 있다.  
일반적으로 사용되는 `while`과 `do...while` 두 가지 반복문에 다뤄보고자 한다.

> 위 두 가지 반복문의 차이점은 조건을 평가하는 순서와 반복 실행 방식이다.

### **while**
`while` 루프는 코드 블록과 조건을 포함하는 반복문이다.  
이 조건은 불리언(boolean) 표현식이며, 조건이 참이면 반복문이 실행되며, 조건이 거짓이 되면 반복이 종료된다.

```kotlin
while (condition) {
    // body: do something repetitive
}
```
> 조건이 처음부터 거짓이면 한 번도 실행되지 않을 수 있으며,  
> 조건이 끝까지 참인 경우에 **무한 루프(infinite loop)**에 빠질 수 있다.  
> 무한 루프는 사용자가 특정 입력을 할 때까지 반복하는 등의 특수한 경우에서 사용된다.

#### **예제 1**
```kotlin
fun main() {
    var i = 0           // 변수 선언
    
    while (i < 5) {     // i가 5 미만 일 때까지
        println(i)      // i를 출력
        i++            // i에 1을 더함
    }
    
    println("Complete")
}
```

위 프로그램은 `i < 5`가 거짓이 될 때까지 `i`를 출력하는 프로그램이다.  
`i`는 `while` 반복문 내에서 1씩 증가되며, `i`가 5가 되면 프로그램은 `Complete`를 출력하며 종료된다.  

#### **예제 2**
```kotlin
fun main() {
    var letter = 'A'        // 변수 선언
    
    while (letter <= 'Z') { // letter가 Z가 될 때까지
        print(letter)       // letter을 이어서 출력
        letter++            // letter를 한 단계 증가
    }
}
```

위 프로그램은 `A` 부터 알파벳을 한 단계씩 증가시키면서 `Z`까지 출력한다.
출력 결과는 다음과 같다.

```text
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

> 문자(`char`)도 `++` 연산자를 사용하여 Unicode 순서대로 증가 시킬 수 있다.
{: .prompt-tip }

#### **예제 3**
다음은 사용자가 입력한 여러 개의 단어를 읽고 출력하는 프로그램이다.

```kotlin
import java.util.*

fun main() {
    val scanner = Scanner(System.`in`) // 표준 입력을 사용하여 사용자의 입력을 읽는 scanner 객체 생성
    
    while (scanner.hasNext()) { // hasNext()는 사용자 입력 중 더 읽을 데이터가 있는지 확인
        val next = scanner.next() // hasNext()가 true 이면 next()로 다음 데이터를 읽음
        println(next)
    }
}
```

**입력 예시**
```text
Kotlin is a modern language
```

**출력 결과**
```text
Kotlin
is
a
modern
language
```

> 숫자 입력 시, scanner.hasNextInt()로 숫자 데이터를 읽을 수 있음.
{: .prompt-tip }

### **do...while**
`do...while` 반복문은 조건을 검사하기 이전에 코드 블록을 최소 1회 실행하는 반복문이다.  
따라서, 반드시 한 번은 실행되는 것이 특징이다.  

```kotlin
do {
    // body: do something
} while (condition)
```

#### **예제 1**
다음은 사용자의 입력을 받아 0이 입력될 때 까지 숫자를 출력하는 프로그램이다.

```kotlin
fun main() {
    do {
        val n = readln().toInt()
        println(n)
    } while (n > 0)
}
```

**입력 예시**
```text
1
2
4
0
```

**출력 결과**
```text
1
2
4
0
```

> `do...while` 구문은 입력값이 최소 1회가 필요한 상황에서 유용하다.
{: .prompt-tip }

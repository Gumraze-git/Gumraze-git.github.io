---
title: "[Introduction to Kotlin] 코틀린 컨벤션"
date: 2025-01-07 10:00:00 +0900
layout: post
category: Kotlin
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Convention is convention
pin: false
---

- - -
## **시작하면서**

처음 프로그래밍을 알게되었을 때 기본 문법 및 논리 구조 등을 이해하는데 어려움이 있었지만, 구현하고 싶은 것을 직접 구현할 수 있다는 것이 매우 흥미로웠다.
나의 전공은 산업공학이지만, 전공 공부보다 종종 즐겁게 공부했고 결국 전공 관련 프로젝트를 구현할 때에도 많은 도움이 되었다.
지금까지는 문법이 틀리지 않는 수준에서 구현을 목적으로 코드를 작성했다.
그래서 나의 코드를 내가 읽기도 어려운 수준이었지만 결국에는 구현할 수 있었기에 큰 문제가 되지 않았다.

그러나 이제 프로그래밍을 업으로 삼고 살아가고자 한 뒤 부터 나의 코드를 누군가에게 공유하고 나도 다른 사람의 코드를 읽어야했다.
언어에 문법과 맥락이 있듯이, 프로그래밍 언어에도 문법과 맥락이 있다고 생각한다.  

**여기서 Convention은 문법이 아니라 맥락이라고 생각한다.**

문법을 지키면서 좋은 맥락을 가진 글을 작성하기 위해서는 해당 언어의 convention을 잘 숙지하고 있어야 한다고 생각한다.
이번에는 Kotlin의 Convention을 공부하고 정리한 내용을 공유하고자 한다.

- - -
## **Convention??**
프로그래머는 처음부터 코드를 작성하는 것보다 다른 개발자가 작성한 코드를 읽는 데 더 많은 시간을 사용한다.
그렇기 때문에 코드를 명확하고 간결하게 작성하는 것은 매우 중요하다.

코드 스타일 규칙, 즉 컨벤션은 읽기 쉬운 코드를 표준화하고 유지하는데 도움이 된다.
> 이러한 규칙은 엄격한 규칙이라기 보다는 권장사항에 가깝다.    
> 나는 컨벤션을 아주 강한 권장사항이라고 생각한다.

대부분의 프로그래밍 언어는 이러한 규칙을 가지고 있으며, 코틀린도 예외는 아니다.

> 모든 규칙을 한 번에 습득할 필요는 없으나, 새로운 개념을 배울 때 마다 이 규칙을 다시 참고하면 된다.  
> 공식 문서에서 이러한 규칙을 확인할 수 있다.

- - -
## **[Kotlin Code Convention](https://kotlinlang.org/docs/coding-conventions.html) 문서 내용 정리**
- - -
### **스타일 가이드 적용하기**
Kotlin을 지원하는 두 IDE - InteliJ IDEA와 Android Studio는 Kotlin 코드 스타일에 대한 지원을 한다.

스타일 가이드를 적용하기 위해 아래 지침을 따르면 된다.
1. 설정/환경 설정 -> 편집기 -> Kotlin으로 이동한다.
2. Set from...을 클릭한다.
3. Kotlin 스타일 가이드를 선택한다.

- - -
### **스타일 가이드 검사하기**
코드가 스타일 가이드를 따르는지 검사하기 위해, IDE에서 아래 방법을 지원한다.
1. 설정/환경 설정 -> 편집기 -> 검사 -> 일반으로 이동한다.
2. 잘못된 서식(Incorrect formatting)을 켠다.

- - -
### **소스 코드 구성**
- - -
#### **디렉토리 구성하기**
Kotlin 프로젝트는 공통 루트 패키지가 생략된 패키지 구조를 따른다.

> 공통 루트 패키지(common root package): 프로젝트의 모든 파일이 공통적으로 시작하는 최상위 패키지를 의미함.  

공통 루트 패키지를 사용하게 되면 코드 파일이 다른 프로젝트의 파일과 충돌하지 않도록 지원하지만,  
폴더가 지나치게 많아질 수 있다.

##### **예시**
- 프로젝트 이름: MyApp  
- 회사 도메인: MyCompany.com  
- 공통 루트 패키지: com.mycompany.myapp  

```text
src/
  └── main/
        └── kotlin/
              └── com/
                    └── mycompany/
                          └── myapp/
                                └── utils/
                                      └── MyUtils.kt
```

위 구조에서 **공통 루트 패키지(com.mycompany,myapp)을 디렉토리 구조에서 생략하면, 더 간단하게 구성 가능하다.**

```
src/
 └── main/
      └── kotlin/
           └── utils/
                └── MyUtils.kt
```

공통 루트 패키지를 디렉토리 구조에서 생략하는 것이 가능한 이유는 Kotlin 컴파일러는 디렉토리 구조를 직접 사용하는 것이 아니라 **package 선언을 기반으로 파일의 위치를 판단**하기 때문이다.  

**즉, 파일이 어느 디렉토리에 저장되어 있던지 `package com.mycompany.myapp.utills` 하고 선언하면 해당 파일은 논리적으로 패키지에 속한 파일로 처리된다.** 

- - -
#### **소스 파일 이름 설정하기**
Kotlin 파일에 단일 클래스 또는 인터페이스가 포함된 경우 해당이름은 클래스 이름과 동일해야하며, `.kt` 확장자가 추가되어야 한다.

파일에 여러 클래스 또는 최상위 선언만 포함된 경우 파일에 포함된 내용을 설명하는 이름을 선택 및 지정한다.  
각 단어의 첫 글자를 대문자로 시작하는 대문자 카멜 케이스를 사용한다. -> `ProcessDeclarations.kt`

> 파일 이름은 파일 내 코드가 무엇을 하는지 설명해야하며, 따라서 `Util`등의 의미없는 단어는 사용되지 않아야 한다.
{: .prompt-info }

- - -
#### **멀티플랫폼(Multiplatform) 프로젝트**
멀티 플랫폼 프로젝트에서는 플랫폼별 소스 세트의 최상위 선언이 있는 파일에는 소스 세트의 이름과 연결된 접미사가 있어야 한다.
- 예시
  - jvmMain/kotlin/Platform.**jvm**.kt
  - androidMain/kotlin/Platform.**andriod**.kt
  - iosMain/kotlin/Platform.**ios**.kt

공통 소스 세트의 경우, 최상위 선언이 있는 파일에는 접미사가 없어야 한다.
- 예시
  - **commonMain**/kotlin/**Platform**.kt

- - -
#### **소스 파일 구성하기**
Kotlin 소스 파일에 여러 선언(클래스, 최상위 함수 또는 프로퍼티)를 배치하는 것은 권장된다.  
단, 이러한 선언들이 의미적으로 밀접하게 된련되어 있고, 파일 크기가 적절한 범위(수백 줄을 초과하지 않는 수준)내에 머물러야 한다.

특히, 모든 클라이언트가 관련된 클래스에 대한 확장 함수(extension function)를 정의할 때,
해당 클래스를 포함한 파일에 확장 함수를 함께 배치해야한다.

반면에, 특정 클라이언트에만 의미 있는 확장 함수를 정희할 경우, 그 클라이언트의 코드 옆에 배치한다.
확장 함수만을 담기 위한 별도의 파일을 생성하는 것은 피한다.

- - -
#### **클래스 레이아웃**
클래스의 내용은 다음 순서로 배치하는 것이 좋다.
1. 프로퍼티 선언 및 초기화 블록
2. 부 생성자(secondary constructors)
3. 메서드 선언
4. 동반 객체(companion object)


> **주의 사항**
> - 메서드 선언을 알파벳 순서나 가시성(visibility) 기준으로 정렬하지 않는다.
> - 일반 메서드와 확장 메서드를 분리하지 말고, 관련된 내용을 같이 배치해라.
>   - 이렇게 하면 클래스의 내용을 위에서 아래로 읽을 때 논리적인 흐름을 따라가기 쉽다.
> - 상위 레벨의 내용부터 먼저 작성할지, 하위 레벨부터 작성할지는 선택하고 일관성을 유지해라.
> - 중첩 클래스(nested class)는 해당 클래스를 사용하는 코드 옆에 배치해라.
{: .prompt-danger }

- - -
#### **인터페이스 구현 레이아웃**
인터페이스를 구현할 때, 인터페이스 멤버와 동일한 순서로 구현 멤버를 배치해라.

> 필요한 경우, 구현에 사용되는 추가적인 private 메서드와 섞어서 배치할 수 있다.

- - -
- - -
## **명명규칙(Naming rules)**
Kotlin의 패키지 및 클래스의 명명 규칙은 매우 간단하다.

- 패키지 이름은 항상 소문자이며 밑줄(`_`)를 사용하지 않는다.
  - 예시: `org.example.project`
- 일반적으로 권장되지 않지만 여러 단어를 사용해야하는 경우 단어를 연결하거나 **CamelCase**를 사용하면 된다.
  - 예시: `org.exampl.MyProject`
  
- 클래스와 객체의 이름은 대문자 카멜 표기법을 사용한다.  

  ```kotlin
  open class DeclarationProcessor { /*...*/ }
  
  object EmptyDeclarationProcessor : DeclarationProcessor() { /*...*/ }
  ```

- - -
### **함수 이름**
함수, 속성 및 로컬 변수의 이름은 소문자로 시작하고 밑줄 없이 **카멜 표기법**을 사용한다.
```kotlin
fun processDeclarations() { /*...*/ }
var declarationCount = 1
```

예외로 클래스 인스턴스를 생성하는데 사용되는 팩토리 함수는 추상 변환 유형과 동일한 이름을 가질 수 있다.
```kotlin
interface Foo { /*...*/ }

class FooImpl : Foo { /*...*/ }

fun Foo(): Foo ( return FooImpl() )
```

- - -
### **테스트 메서드 이름**
오직 테스트 코드에서만 백틱(backticks, ``)으로 감싸진 공백이 포함된 메서드 이름을 사용할 수 있다.
> 이러한 메서드 이름은 안드로이드 런타임 API 레벨 30부터 지원됨.

또한, 테스트 코드에서는 메서드 이름에 밑줄(_)을 사용하는 것도 허용된다.

```kotlin
class MyTestCase {
    @Test
    fun `ensure everything works`() { /*...*/ }
  
    @Test
    fun ensureEverythingWorks_onAndroid() { /*...*/ }
}
```

### **속성(property) 이름**
`Const`로 표시된 상수 또는 최상위 또는 객체(`object`)의 `val` 프로퍼티(사용자 정의 get 함수가 없고 변경 불가능한 데이터를 담고 있는 경우)의 이름은 모두 대문자로 작성하며, 밑줄(`_`)로 단어를 구분한다. 
> 이 형식을 스크리밍 스네이트 케이스(SCREAMING_SNAKE_CASE)라고 부른다.
{: .prompt-info }

```kotlin
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserNAme"
```

**동작이나 변경 가능한 데이터를 포함하는 객체**를 보관하는 최상위 속성이나 객체 속성의 이름은 **카멜 표기법**을 사용해야 한다.
```kotlin
val mutableCollection: MutableSet<String> = HashSet()
```

**싱글톤 객체에 대한 참조를 보유하는 속성**의 이름은 선언과 동일한 명명 스타일을 사용할 수 있다.
```kotlin
val PersonComparator: Comparator<Person> = /*...*/
```

**열거형 상수(enum constants)**의 경우, 사용법에 따라 모두 대문자 또는 밑줄로 구분된 **스크리밍 카멜 케이스**를 사용해도 된다.
```kotlin
enum class Color { RED, GREEN }
enum class SpecificColor { DARK_RED, DARK_GREEN }

```

- - -
### **백킹(backing) 속성 명명법**
클래스에 개념적으로 동일하지만 하나는 공개 API의 일부이고 다른 하나는 구현 세부 사항인 두 개의 속성이 있는 경우 비공개 속성의 이름에 대한 접두사로 밑줄을 사용한다.
```kotlin
class C {
    private val _elementList = mutableListOf<Element>() // 비공개 내부 구현용 프로퍼티

    val elementList: List<Element>                      // 공개 프로퍼티
        get() = _elementList                            // 내부 구현 프로퍼티를 기반으로 값을 제공함.
}
```

- - -
### **좋은 이름 선택하기**
- **클래스의 이름**은 일반적으로 클래스가 무엇인지 설명하는 명사이거나 명사구로 작성하는 것이 좋다.
  - 예시: `List`, `PersonReader`
- **메서드의 이름**은 일반적으로 동사 또는 동사구로 작성하며, 메서드가 무엇을 수행하는지 나타내도록 해야한다.
  - 예시: `close`, `readPerson`
- **메서드의 이름**은 메서드가 객체를 변경하는지(mutate) 또는 새로운 객체를 반환하는지도 암시해야한다.
  - 예시: `sort` 컬렉션은 제자리에서 정렬하는 반면, `sorted` 컬렉션은 정렬된 복사본을 반환해야한다.
- 이름을 통해 해당 엔티티(클래스, 메서드)의 목적이 명확하게 드러나야 하므로 이름에 무의미한 단어(`Manager`, `Wrapper`)는 사용하지 않는 것이 좋다.
- 선언한 이름의 일부로 약어를 사용할 때, 두 글자로 구성된 경우 대문자로 시작하고(`IOStream`), 두 글자가 더 길면 첫 글자만 대문자로 시작한다.(`XMLFormatter`, `HttpInputStream`)

- - -
### **Formatting: 서식 지정**
- - -
#### **들여쓰기(Indentation)**
들여쓰기에는 4개의 공백을 사용한다.
> 탭(tap)을 사용하지 마라.

- - -
#### **중괄호 서식(Curly braces)**
중괄호(curly braces)의 경우, 여는 중괄호는 구문이 시작되는 줄의 끝에 작성하고, 닫는 중괄호는 여는 중괄호와 수평으로 맞추어 별도에 줄에 작성한다.

**사용 예시**
```kotlin
if (elements != null) { // 여는 중괄호는 구문의 시작되는 줄에 작성.
    for (element in elements) { // 들여쓰기는 탭을 사용하지 않고 4개의 공백 사용
      // ...
    } 
} // 닫는 중괄호는 여는 중괄호가 있는 구문과 수평적인 위치와 별도의 줄에 작성한다.
```

- - -
#### **수평 공백(Horizontal whitespace)** 
이진 연산자(binary operatiors)를 사용할 때는 공백을 사용해야한다.
> 범위(range to) 연산자 주위에는 공백을 사용하지 않는다.

**사용 예시**
```kotlin
fun main() {
    val a = 10
    val b = 12
    val c = a + b // 이진 연산자를 사용할 때는 공백 사용.
    val d = b+c // 규칙 위반.
}
```

단항 연산자 주위에는 공백을 사용하지 않는다.
```kotlin
fun main() {
    var a = 5
    println(a++) // 단항 연산자 주위에는 공백을 사용하지 않음.
}
```

제어 흐름 키워드(`if`, `when`, `for`, `while`)와 해당 제어 흐름을 여는 괄호 사이에 공백을 넣는다.
```kotlin
fun main() {
    val number = 10
    if (number > 0) { // 제어 흐름을 여는 괄호는 공백 추가 후 작성함.
        println("Positive Number")
    }
}
```

주 생성자 선언, 메서드 선언 또는 메서드 호출에서 여는 소괄호(parenthesis) 앞에 공백을 넣지 않는다.
```kotlin
class A(val x: Int) // 주 생성자 선언 "A" 뒤 소괄호는 공백을 넣지 않고 붙여 작성한다.

fun foo(x: Int) { ... } // 메서드 선언

fun bar() {
    foo(1)
}
```

`(`, `)`, `[`, `]` 뒤에 공백을 넣지 않는다.
```kotlin
println("No space")
```

`.`, `?.` 주위에 공백을 넣지 않는다.
```kotlin
foo.bar().filter { it > 2 }.joinToString()
foo?.bar()
```

`//` 뒤에는 공백을 넣는다.
```kotlin
// 이것은 주석입니다.
```

`::`주위에는 공백을 넣지 않는다.
```kotlin
Foo::class
String::length
```

nullable 타입을 나타내기 위해 사용되는 `?` 앞에는 공백을 넣지 않는다.
```kotlin
String?
```

일반적인 규칙으로, 수평 정렬(horizontal alignment)을 피하라.

```kotlin
// 잘못된 예시
val short   = 5
val longer  = 10
val longest = 20

// 올바른 예시
val short = 5
val longer = 10
val longest = 20
```
> 코드의 정렬보다는 일관된 들여쓰기와 간결한 구조를 우선 시 하는 것이 유지보수 시 용이하다.

- - -
#### **콜론(:)**
- 아래 상황에서는 `:` 앞에 공백을 넣는다.
  - 타입과 슈퍼타입(supertype)을 구분할 때.
    - 타입은 변수, 객체, 함수 등이 가질 수 있는 데이터의 종류를 의미한다.
    - 슈퍼타입은 클래스나 인터페이스 간의 계층 구조에서 더 상위에 있는 타입을 의미한다.
      ```kotlin
      // Animal은 슈퍼타입
      open class Animal {
          fun eat() {
              println("This animal eats food.")
          }
      }
      
      // Dog은 Animal을 상속받은 서브타입
      class Dog : Animal() { 
          fun bark() {
              println("Woof!")
          }
      }
      
      fun main() {
          val myDog: Dog = Dog() // Dog 타입
          myDog.eat() // 슈퍼타입 Animal의 메서드 사용
          myDog.bark() // 서브타입 Dog의 메서드 사용
      }
      ```    

  - 슈퍼클래스(super class) 생성자 또는 같은 클래스의 다른 생성자에 위임 할 때.  
    ```kotlin
    open class Animal(val name: String)
    
    class Dog(name: String, val breed: String) : Animal(name) { // 생성자 위임 시 `:` 앞에 공백
    constructor(name: String) : this(name, "Unknown") // 같은 클래스의 다른 생성자로 위임
    }
    ``` 
  - object 키워드 뒤에 사용할 때.

    ```kotlin
    val myObject = object : Runnable { // object 키워드 뒤에 `:` 앞에 공백
        override fun run() {
            println("Running...")
        }
    }
    ```
  - 아래 상황에서는 `:` 앞에 공백을 넣지 않는다.
    - 선언(declaration)과 타입(type)을 구분할 때.

      ```kotlin
      val name: String = "Kotlin" // 선언과 타입 사이에는 `:` 앞에 공백 없음
      val age: Int = 25
      ```
- 일반적으로 항상 `:`뒤에는 공백을 넣는다.

- - -
#### **클래스 헤더(Class Header)**
몇 개의 기본 생성자 매개변수가 있는 클래스는 한 줄로 작성할 수 있다.
```kotlin
class Person(id: Int, name: String)
```

헤더가 긴 클래스는 각 기본 생성자 매개변수가 들여쓰기가 있는 별도의 줄에 있도록 작성해야한다.
또한, 상속을 사용하는 경우 슈퍼클래스 생성자 호출 또는 구현된 인터페이스 목록은 괄호와 같은 줄에 있어야 한다.
```kotlin
class Person(
    id: Int,
    name: String,
    height: Int,
    weight: Int
) : Human(id, name) { /*...*/ } // 상속을 사용하는 슈퍼 클래스 생성자.
```

여러 인터페이스가 있는 경우 슈퍼클래스 생성자 호출을 먼저 작성한 뒤, 다음 각 인터페이스를 다른 줄에 작성한다.
```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(), // 슈퍼클래스
    SomeOtherInterface, // 인터페이스 1
    AndAnotherOne {     // 인터페이스 2

  fun foo() { /*...*/
  }
}
```

긴 상위 유형 목록이 있는 클래스의 경우 콜론 뒤에 줄 바꿈을 넣고 모든 상위 유형의 이름을 가로로 맞춘다.
```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne {

    fun foo() { /*...*/ }
}
```

클래스 헤더가 긴 경우에 클래스 해더와 본문을 구분하기 위해 클래스 헤더 뒤에 빈 줄을 넣거나(위의 예시 처럼) 여는 중괄호는 별도의 줄에 넣는다.
```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne
{
    fun foo() { /*...*/ }
}
```

- - -
### **수정자 순서(Modifiers order)**
선언에 여러 개의 수정자가 있는 경우, 항상 다음 순서에 따라 배치해라.
```text
public / protected / private / internal
expect / actual
final / open / abstract / sealed / const
external
override
lateinit
tailrec
vararg
suspend
inner
enum / annotation / fun // as a modifier in `fun interface`
companion
inline / value
infix
operator
data
```

**모든 애너테이션(annotation)은 수정자 앞에 둔다.**
```kotlin
@Named("Foo")
private val foo: Foo
```

- - -
### **애너테이션(Annotations)**
애너테이션은 선언문 앞에 별도 줄에 동일한 들여쓰기로 배치한다.
```kotlin
@Target(AnnotationTarget.PROPERTY)
annotation class JsonExclude
```

인수가 없는 애너테이션은 같은 줄에 배치할 수 있다.
```kotlin
@JsonExclude @JvmField
var x: String
```

인수가 없는 단일 애너테이션은 해당 선언과 같은 줄에 배치될 수 있다.
```kotlin
@Test fun foo() { /*...*/ }
```

- - -
### **파일 애너테이션(File annotations)**
파일 애너테이션은 파일 주석 뒤, 패키지 선언 앞에 위치하며, 패키지와는 빈 줄로 구분한다.
> 이는 애너테이션이 패키지가 아닌 파일을 대상으로 한다는 점을 강조하기 위함이다.

```kotlin
/** License, copyright and whatever */
@file:JvmName("FooBar")

package foo.bar
```

- - -
### **함수(function)**
함수의 서명(signature)가 단일 줄에 작성되지 않는 경우에 아래와 같이 작성한다.
```kotlin
fun longMethodName(
    argument: ArgumentType = defaultValue,
    argument2: AnotherArgumentType,
): ReturnType {
    // body
}
```

본문이 **단일 표현식으로 구성된 함수의 경우 표현식 본문을 사용**하는 것이 더 좋다.
```kotlin
fun foo(): Int {     // bad
    return 1
}

fun foo() = 1        // good
```

- - -
### **표현식 본문(Expression bodies)**
함수의 표현식 본문의 첫 줄이 선언과 같은 줄에 맞지 않은 경우, 첫번 째 줄에 `=`부호를 넣고 표현식 본문을 4칸 들여쓴다.
```kotlin
fun f(x: String, y: String, z: String) =
    veryLongFunctionCallWithManyWords(andLongParametersToo(), x, y, z)
```

- - -
### **속성(Properties)**
매우 간단한 읽기 전용 속성의 경우 한 줄 서식을 고려한다.
```kotlin
val isEmpty: Boolean get() = size == 0
```

더 복잡한 프로퍼티의 경우, 항상 `get`과 `set` 키워드를 별도의 줄에 작성한다.
```kotlin
val foo: String
    get() { /*...*/ }
```

초기화식(initializer)이 있는 프로퍼티에서 초기화 식이 긴 경우, `=`기호 뒤에 줄 바꿈을 추가하고 초기화 식을 4칸 들여쓰기 한다.
```kotlin
private val defaultCharset: Charset? =
    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

### **제어 흐름 문장(Control flow statements)** 
`if` 또는 `when`문의 조건이 여러줄 일 경우, 항상 중괄호를 사용하여 본문을 감싸야한다.
조건문의 각 줄(statement)는 시작 위치에서 4칸 들여쓰기 해야한다.
조건문을 닫는 괄호와 본문을 여는 중괄호는 별도의 줄에 함께 작성함.

```kotlin
if (!component.isSyncing &&
    !hasAnyKotlinRuntimeInScope(module)
) { // 조건문을 닫는 괄호와 본문을 여는 중괄호는 별도의 줄에 함께 작성함.
    return createKotlinNotConfiguredPanel(module)
}
```

루프의 `else` 키워드 뿐만 아니라, `catch`, `finally`, `while` 키워드는 이전 중괄호와 같은 줄에 작성한다.

```kotlin
if (condition) {
    // 본문
} else { // 이전 중괄호와 같은 줄에 작성
    // else 부분
}

try {
    // 본문
} finally { // 이전 중괄호와 같은 줄에 작성
    // 정리 작업
}
```

`when`문의 각 분기(branch)가 여러 줄로 구성된 경우, 인접한 분기 블록과 빈 줄로 구분하는 것을 권장한다.
```kotlin
private fun parsePropertyValue(propName: String, token: Token) {
    when (token) {
        is Token.ValueToken ->
            callback.visitValue(propName, token.value)

        Token.LBRACE -> { 
            // ...
        }
    }
}
```

짧은 분기(branch)의 경우, 중괄호 없이 조건과 같은 줄에 작성한다.

```kotlin
when (foo) {
    true -> bar() // 좋음
    false -> { baz() } // 나쁨
}
```

- - -
### **메서드 호출(Method calls)**
긴 인자(argument) 목록이 있는 경우, 여는 괄호 뒤에 줄바꿈을 삽입하고, 인자를 4칸 들여쓰기 한다.
또한, 서로 밀접하게 관련된 인자들은 한 줄에 그룹화 한다.
```kotlin
drawSquare(
    x = 10, y = 10,
    width = 100, height = 100,
    fill = true
)
```
> 인자 이름과 값 사이의 `=` 기호 주변에는 공백을 추가한다.

- - -
### **체인으로 결합되어 있는 호출(Warp chained calls)**
체인으로 결합되어 있는 호출을 줄바꿈 할 때, `.` 또는 `?.` 연산자를 다음 줄로 이동시키고, 한 번 들여쓰기 한다.

```kotlin
val anchor = owner
    ?.firstChild!!
    .siblings(forward = true)
    .dropWhile { it is PsiComment || it is PsiWhiteSpace }
```

- - -
### 람다 표현식(Lambdas)
람다 표현식에서 중괄호와 화살표 `>` 주변에 공백을 추가한다.
단일 람다를 전달하는 경우, 가능한 괄호 바깥으로 전달한다.

```kotlin
list.filter { it > 10 }
```

람다에 레이블을 지정하는 경우, 레이블과 여는 중괄호 사이에는 공백을 넣지 않는다.
```kotlin
fun foo() {
    ints.forEach lit@{
        // ...
    }
}
```

여러 줄로 구성된 람다에서 매개변수 이름은 첫 줄에 작성하고, 화살표와 줄바꿈을 뒤 따르게 한다.
```kotlin
appendCommaSeparated(properties) { prop ->
    val propertyValue = prop.get(obj)  // ...
}
```

매개변수 목록이 너무 길어서 한 줄에 넣기 어려운 경우에는 화살표를 별도의 줄에 작성한다.
```kotlin
foo {
   context: Context,
   environment: Env
   ->
   context.configureEnv(environment)
}
```

- - -
### **후행 쉼표(Trailing commas)**
후행 쉼표는 요소 목록의 마지막 항목 뒤에 오는 쉼표를 의미한다.
```kotlin
class Person(
    val firstName: String,
    val lastName: String,
    val age: Int, // 후행 쉼표
)
```

후행 쉼표를 사용하는 것은 아래와 같은 이점이 있다.
- 버전 관리 도구의 변경 내역(diff)이 간결해지고, 변경된 값에만 집중할 수 있다.
  - **후행 쉼표 사용 전 예시**
    ```kotlin
    class Person(
        val firstName: String,
        val lastName: String
    )
    ```
    **새로운 항목 추가 후:**
  
    ```diff
    class Person(
         val firstName: String,
    -    val lastName: String
    +    val lastName: String,
    +    val age: Int
    )
    ```
    
  - **후행 쉼표 사용 후 예시**
    ```kotlin
    class Person(
        val firstName: String,
        val lastName: String, // 후행 쉼표
    )
    ```
    
    **새로운 항목 추가 후:**
    ```diff
    class Person(
        val firstName: String,
        val lastName: String,
    +   val age: Int,
    )
    ```
    >   이전 줄이 변경되지 않으므로, 변경된 부분에만 집중할 수 있다.

- 요소를 추가하거나 재배치하기 쉬워지며 쉼표를 추가하거나 삭제할 필요가 없다.
  - 후행 쉼표 사용 전
    ```kotlin
    val list = listOf(
        "Apple",
        "Banana"
    )
    ```  
  
  - 새로운 요소 추가할 경우의 용의성
  ```kotlin
    val list = listOf(
        "Apple",
        "Banana",
        "Cherry"
    )
    ```
- 코드 생성이 간소화된다.
  - 위의 예시와 같이 작성하게 되면 코드의 자동 생성 로직 또한 단순해지고 유지보수가 용이해진다.

> 후행 쉼표는 선택사항이며 사용하지 않아도 코드는 정상적으로 작동한다.  
> Kotlin 스타일 가이드는 선언 위치에서 후행 쉼표를 사용할 것을 권장하며 호출 위치에서는 사용 여부를 개발자 재량에 맡긴다.

## 세 줄 요약
- Kotlin convention 문서에서 우선 기본적인 코딩을 위한 규칙들은 다룬 것 같다.
- 이외에도 문서형 주석 등의 몇 가지 정리하지 않은 컨벤션은 추후 내가 코딩 공부를 하면서 정리의 필요성을 느낄 때, 다시 한번 정리할 예정이다.
- 위 내용으로도 충분히 기본적인 컨벤션을 익힐 수 있을 것 같으며, 이것들을 익히는데에도 꽤 시간이 걸릴 것 같다.

# 참고문헌
- [Coding convention](https://kotlinlang.org/docs/coding-conventions.html#guard-conditions-in-when-expression)

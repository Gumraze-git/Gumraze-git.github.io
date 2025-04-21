---
title: "[Introduction to Kotlin] 변경 가능한 리스트"
date: 2025-04-25 10:00:00 +0900
layout: post
category: [Kotlin]
comments: true
tag: [Kotlin]
image:
  path: assets/attachment/kotlin_study/kotlin_logo.png
description: Mutable list of Mutalisk 
pin: false
---
- - -

## List
Kotlin은 리스트를 다루고 내용을 수정할 때 유용한 함수를 제공한다.  

### 리스트 출력하기
`joinToString()`은 `separator` 속성을 이용하여 리스트를 다양한 방식으로 출력하는데 도움이 된다.  
기본적으로 `joinToString()`은 `mutableList`의 요소를 저장된 순서대로 가져와서 쉼표로 구분된 문자열으로 변환한다.

```kotlin
val southernCross = mutableListOf("Acrux", "Gacrux", "Imai", "Mimosa")
println(southernCross.joinToString())   // Acrux, Gacrux, Imai, Mimosa
```

또한, `joinToString()`의 인자로 구분자를 변경 할 수 있다.
```kotlin
println(southernCross.joinToString(" -> "))
```

### 여러 개의 리스트 다루기
여러 개의 리스트를 하나로 합칠 수 있다.

```kotlin
val southernCross = mutableListOf("Acrux", "Gacrux", "Imai", "Mimosa")
val stars = mutableListOf("Ginan", "Mu Crucis")

val newList = southernCross + stars // + 연산자로 두 개의 mutableList를 하나로 합칠 수 있음
println(newList.joinToString())    // Acrux, Gacrux, Imai, Mimosa, Ginan, Mu Crucis
```
또한, 여러 개의 리스트를 `==`과 `!=` 연산자로 크기와 내용을 비교할 수 있다.

```kotlin
val firstList = mutableListOf("result", "is", "true")
val secondList = mutableListOf("result", "is", "true")
val thirdList = mutableListOf("result")

println(firstList == secondList)  // true
println(firstList == thirdList)   // false
println(secondList != thirdList)  // true
```

> 두 리스트의 모든 요소가 같은 순서로 포함되어 있어야 `true`를 반환한다.

### 리스트 내용 변경하기
Kotlin의 `val`과 `var`키워드는 변수의 값이나 참조를 어떻게 다룰지 결정한다.  

- `var`: 변수의 값 또는 참조를 변경함
- `val`: 변수의 값 또는 참조를 한 번만 할당 가능하며, 실행 중 변경할 수 없음

그러나 `val`을 사용하더라도 리스트의 기존 요소를 수정하는 것은 가능하다.  
이는 리스트의 내용일 변경될 뿐 새로운 리스트가 생성되는 것이 아니기 때문이다.  

```kotlin
val southernCross = mutableListOf("Acrux", "Gacrux", "Imai", "Mimosa") // val으로 선언
var stars = mutableListOf("Ginan", "Mu Crucis") // var으로 선언

southernCross[1] = "star"
stars[1] = "star"

println(southernCross[1]) // star
println(stars[1]) // star
```

### 리스트 요소 추가 및 삭제
`add`, `remove`, `clear` 함수를 사용하여 리스트를 변경할 수 있다.

```kotlin
val southernCross = mutableListOf("Acrux", "Gacrux", "Imai", "Mimosa")
val stars = mutableListOf("Ginan", "Mu Crucis")
val names = mutableListOf("Jack", "John", "Katie")
val food = mutableListOf("Bread", "Cheese", "Meat")
val fruits = mutableListOf("Apple", "Banana", "Grape", "Mango")

southernCross.removeAt(0)
southernCross.remove("Mimosa")

stars.add("New star")
stars.add(0, "First star")

names.clear()

food.addAll(fruits)

println(names) // []
println(southernCross.joinToString()) // Gacrux, Imai
println(stars.joinToString()) // First star, Ginan, Mu Crucis, New star
println(food.joinToString()) // Bread, Cheese, Meat, Apple, Banana, Grape, Mango
```
각각의 사용법을 살펴보자
- remove
  - `removeAt(index)`: 특정 인덱스의 요소 삭제
  - `remove(element)`: 특정 요소 삭제
- add
  - `add(element)`: 리스트 끝에 요소 추가
  - `add(index, element)`: 특정 위치에 요소 추가
  - `addAll(list)`: 다른 리스트의 모든 요소를 추가
- clear
  - `clear()`: 리스트의 모든 요소 삭제 

또한, `+=` 연산자로 요소를 추가 할 수 있다.

```kotlin
val vowels = mutableListOf('a', 'o', 'i', 'e', 'u')
val intList1 = mutableListOf(1, 2, 3, 4, 5)
val intList2 = mutableListOf(5, 4, 3, 2, 1)

vowels += 'y'
intList1 += intList2

println(vowels)   // [a, o, i, e, u, y]
println(intList1) // [1, 2, 3, 4, 5, 5, 4, 3, 2, 1]
```

### 리스트 복사하기
Kotlin에는 리스트를 복사하는 기본 함수가 없지만, `toMutableList()`를 사용하여 복사 할 수 있다.

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
val copyList = list.toMutableList()

print(copyList) // [1, 2, 3, 4, 5]
```

### 추가적인 유용한 함수들
- `list.isEmpty()` 그리고 `list.isNotEmpty()`: 리스트가 비어있는지 확인
- `list.subList(from, to)`: 특정 범위의 하위 리스트 생성
- `list.indexOf(element)`: 특정 요소의 인덱스 반환
- `list.minOrNull()` 그리고 `list.maxOrNull()`: 최소/최대 값 찾기
- `list.sum()`: 리스트의 모든 요소 합산
- `list.sorted()` 그리고 `list.sortedDescending()`: 리스트 정렬

```kotlin
val numbers = mutableListOf(1, 2, 3, 4, 5)
val vowels = mutableListOf('e', 'a', 'y', 'i', 'u', 'o')

println(numbers.minOrNull()) // 1
println(numbers.maxOrNull()) // 5
println(numbers.sum())      // 15

println(vowels.sorted()) // [a, e, i, o, u, y]
println(vowels.sortedDescending()) // [y, u, o, i, e, a]
```

---
comments: true
---

# Kotlin - Funtions

코틀린에서 정수(Int)를 반환하는 함수는 다음과 같습니다.

```kotlin
fun sum(): Int {
    return 2 + 3
}
```

정수 매개 변수 `a`, `b`를 받고 정수를 반환하는 함수는 다음과 같습니다.

```kotlin
fun sum(a: Int, b: Int) { // 반환 타입은 생략할 수 있습니다.
    return a + b
}
```

!!! tip "자바와 다른 점"

    자바는 반환 타입을 생략할 수 없습니다.

함수 본문은 표현식(expression)이 될 수 있습니다.

```kotlin
fun sum(a: Int, b: Int) = a + b
```

아무 것도 반환하지 않을 때는 `Unit`으로 표기하나, 익명이나 람다로 사용하는 경우가 아니면 생략합니다.

!!! tip "자바와 다른 점"

    자바는 아무것도 반환하지 않을 때 `void`입니다.

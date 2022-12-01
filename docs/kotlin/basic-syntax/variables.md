---
comments: true
---

# kotlin - var, val

kotlin에서 변수는 `var` 또는 `val` 키워드를 앞에 적고 선언된 것을 의미합니다.

```kotlin
val a = "변수 a" // String 타입 불변 변수
var b = 3 // Int 타입 가변 변수
```

!!! tip "Java와 다른 점"

    과거의 Java는 변수를 선언할 때 항상 타입을 명시해야 했습니다.

    ```java title="Example.java"
    String a = "변수";
    ```

    그러나 Kotlin은 타입 추론이 가능하여 일부 상황에서 타입을 선언하지 않습니다.

## var 변수

```kotlin
var a = "변수"
```

var 키워드로 선언된 변수는 가변(mutable)입니다.

따라서, 언제든지 값이 변할 수 있는 변수에 사용합니다.

기본적인 java의 변수 사용법과 동일합니다. JDK 10이상에서는 변수를 선언할 때 타입 추론이 가능해져 사실상 똑같습니다.

주의할 점은 한 번 '**타입 추론이 이루어진 변수는 타입을 변경할 수 없습니다**'.

```kotlin
var a = "문자열 변수"
a = 1 // 에러: String 변수에 Int 값을 대입할 수 없습니다.
```

!!! tip "Java와 다른 점"

    java의 대입(expression[^1])과 달리 kotlin의 대입은 문(statement[^2])입니다.

    ```java title="Example.java"
    a = b = c // expression이므로 가능
    ```

    ```kotlin title="Example.kt"
    a = b = c // statement이므로 불가능
    ```

    kotlin은 expression이 굳이 필요한 이유가 없어 지원하지 않습니다.

## val 변수

`val` 키워드로 선언된 변수는 불변(immutable)입니다.

따라서 읽기 전용(Read-Only) 변수라고 부르기도 합니다.

```kotlin
val b = "불변 변수"
```

`var` 변수와 다른 점은 불변이기 때문에 '**선언과 동시에 초기화가 반드시 이루어져야 한다**'는 것입니다. 이는 java의 `final` 키워드를 사용했을 때와 같습니다.

```kotlin
val b: String // 컴파일 에러
```

## 최상위 변수

최상위에 변수를 선언할 수 있고, 이 변수는 어느 곳에서나 접근 가능합니다.

```kotlin
val PI = 3.14

fun printPI() {
    println(PI)
}
```

[^1]:
    expression은 수식이라는 의미이며, 이 의미는 항상 하나 이상의 값으로 표현된다는 것입니다. 예를 들어, `1 + 2`라는 수식은 `3`이라는 결과가 항상 존재합니다.
[^2]:
    statement는 서술이라는 의미이며, 이 의미는 실행 가능(executable)한 가장 작은 단위입니다. if 문이나 when 문과 같이 조건문, 반복문 등은 실제로 아무런 값을 주지 않으며 그렇기에 최소 하나의 expression과 같이 쓰이는 경우가 대부분입니다.

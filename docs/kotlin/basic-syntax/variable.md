---
title: val
description: >-
    Kotlin에서 변수를 선언하는 방법에 대해 소개합니다.
comments: true
---

# 코틀린 - val

## 변수 선언

```kotlin
val a = "변수"
```

!!! tip "Java와 다른 점"

    과거의 Java는 변수를 선언할 때 항상 타입을 명시해야 했습니다.

    ```java title="example.java"
    String a = "변수"; # (1)!
    ```

    1.  Kotlin에서 세미콜론(;)은 불필요한 존재에 해당

    그러나 Kotlin은 타입 추론이 가능하여 일부 상황에서 타입을 선언하지 않습니다.

```
String a = "변수";
# (1)!
```

1.  Kotlin에서 세미콜론(;)은 불필요한 존재에 해당

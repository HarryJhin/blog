---
comments: true
---

# Kotlin - Entry Point

kotlin 파일의 실행 시작점은 `main` 함수입니다.

```kotlin
fun main() {
    // 시작점
}
```

실행할 때 매개 변수를 입력 받을 수 있습니다.

```kotlin
fun main(args: Array<String>) {
    println(args.contentToString())
}
```

!!! tip "Java와 다른점"

    Java 파일의 시작점도 같은 `main()` 메서드입니다.

    단지 java의 메서드는 단독으로 존재하지 못하기 때문에 항상 class가 있습니다.

    ```java title="Example.java"
    class Example {
        public static void main(String[] args) {
            // 시작점
        }
    }
    ```

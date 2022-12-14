---
title: Kotlin - Overview
description: 코틀린을 사용해야 하는 이유에 대해 설명합니다.
comments: true
---

# 왜 코틀린인가?

Kotlin은 JVM 환경에서 동작하는 언어로 Java를 대체[^1]하기 위해 JetBrains가 개발했습니다.

## 안드로이드 앱 개발

안드로이드 앱 개발은 2019년 Google I/O 이후 Kotlin-first가 되었습니다.

안드로이드 개발자 공식 문서를 확인해보면 대부분의 가이드가 Kotlin으로 작성된 것을 보실 수 있습니다.

또한, 최근에 View(XML) 구조를 버린 Jetpack Compose 라이브러리를 사용하려면 Java가 아닌 Kotlin이 반강제가 되면서 더더욱 가파른 상승세를 보이고 있습니다.

사실 Java로 충분하지 않냐고 하실 수 있지만 안드로이드는 서버(스프링) 생태계보다 급진적인 곳입니다. 구글 플레이스토어는 매년 11월부터 앱 개발의 중요한 Target SDK 버전[^2]을 업그레이드한 앱만 업로드 가능한 정책을 취하고 있기 때문입니다. 따라서 이러한 변화에 맞추어 개발자가 따라가는 것이 중요합니다.

## 현대적이고 간결하며 안전하다

Kotlin은 후발 주자 언어들이 그렇듯이 다른 언어들의 장점을 취하고 단점을 상쇄하는 진화된 고급 언어입니다.

Java에서 엔티티를 작성할 때 우리는 `getter`와 `setter` 그리고 생성자 등을 직접 구현하거나, Gradle 또는 Maven 프로젝트의 경우 Lombok 플러그인을 추가하여 어노테이션을 클래스에 추가하는 방식으로 구현을 해왔습니다.

하지만 Kotlin은 `data class`를 통해서 이 모든 것을 대신 만들어 줍니다.

```kotlin
data class User(
    val name: String = "홍길동", // 기본 값 지정
    val age: Int // val 키워드로 선언된 변수는 초기화된 이후 불변
) // 자동 생성되는 함수: equals(), hashCode(), toString(), copy()

fun main() { // c언어 처럼 main() 함수가 시작점이나, 클래스 필수가 아님
    val user = User(
        age = 7
    ) // 객체를 생성하는데 new 키워드가 필요하지 않음
    println(user) // 자동 생성된 toString() 사용
}
```

위 코드를 보시면 불필요하게 쓰는 어노테이션 또는 함수 없이 자동으로 구현하는 키워드를 통해 다른 Java 코드보다 훨씬 코드양을 줄이면서도 그 의도를 더욱 명확하게 이해할 수 있게 해줍니다.

이러한 것으로 하여금 개발자는 코드를 작성하면서 행복함(?)을 느낄 수 있습니다.

## 서버 애플리케이션 작성에 생산적이다

Kotlin은 기존 Java 기반 기술 스택과 완전한 상호 호환성을 유지하면서 간결하고 풍부한 표현력으로 작성할 수 있습니다.

대표적으로 Java 애플리케이션인 스프링을 코틀린으로 개발할 수 있습니다.

Kotlin을 사용하여 개발 가능한 서버 프레임워크:

- Spring / Spring Boot
- Ktor

이 외에도 다양한 프레임워크가 지원되나 대표적인 2가지만 뽑았습니다.

[^1]:
    Java 프로젝트를 소유한 Oracle이 JDK 유료화를 선언하면서, 많은 기업이 OpenJDK로 엑소더스가 일어났고, 이는 구글이 이끄는 안드로이드도 마찬가지였습니다.
[^2]:
    새로운 안드로이드 버전이 출시될 때마다 기존 버전과 정책이 달라지는 경우가 많습니다. 이는 발전하는 하드웨어와 강화되는 사용자 보안때문이며, 개발자는 사용자 경험을 위해 최신 안드로이드 버전에서 정상적으로 사용할 수 있도록 개선하는 작업이 필요합니다. 이를 위해 구글은 Playstore의 업데이트 정책을 강제하고 있습니다.

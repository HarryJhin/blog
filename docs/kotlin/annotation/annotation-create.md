---
title: Kotlin - annotation class
description: 코틀린으로 어떻게 어노테이션을 만들 수 있는지 소개합니다. 어노테이션은 메타 데이터를 코드에 첨부하는 수단입니다.
comments: true
---

# Annotions class

어노테이션을 선언하려면 `annotation` 변경자를 앞에 선언합니다.

```kotlin
annotation class Fancy자
```

어노테이션 클래스에 메타 어노테이션을 추가하여 어노테이션의 추가 속성을 지정할 수 있습니다.

- `@Target`은 이 어노테이션을 달 수 있는 종류를 제한합니다. (예를 들어 클래스, 함수, 프로퍼티, 표현식 등)
- `@Retention`은 어노테이션이 컴파일된 클래스 파일에 저장되는지 여부와 런타임에 리플렉션을 통해 표시되는지 여부를 지정합니다. (기본은 둘 다 `true`)
- `@Repeatable`은 단일 요소에서 여러 번 어노테이션을 사용할 수 있도록 허용합니다.
- `@MustBeDocumented`는 주석이 public API의 일부이며, 생성된 API 문서에 표시된 class 또는 method의 시그니쳐에 포함되어야 함을 지정합니다.

```kotlin
@Target(AnnotationTarget.CLASS, AnnotationTarget.FUNCTION,
AnnotationTarget.TYPE_PARAMETER, AnnotationTarget.VALUE_PARAMETER,
AnnotationTarget.EXPRESSION)
@Retention(AnnotationRetention.SOURCE)
@MustBeDocumented
annotation class Fancy
```

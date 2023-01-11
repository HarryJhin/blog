---
title: "안전한 로깅"
description: >-
    "앱 런타임에서 간편하게 현재 상황을 logcat에서 확인할 수 있는 로그는 잠재적인 보안 위험 사항입니다. 이를 해결하려면 어떻게 해야할까요? 바로 `BuildConfig.DEBUG` 값을 활용하는 것입니다."
comments: true
---

# 안드로이드 로깅

안드로이드에서 로그를 남긴 다는 것은 앱이 런타임일 때 제대로 동작하는 지에 대한 검증 방법 중 하나로 널리 사용되고 있습니다.

하지만 이는 잠재적인 보안 이슈사항인거 알고 계셨나요?

바로 `Log` 클래스를 사용한 출력은 Release 환경일 때도 출력됩니다.

보통 Release는 상용 앱의 단계이기 때문에 불특정 다수가 손쉽게 앱의 로그를 접근할 수 있다는 것은 매우 위험한 것입니다.

이를 해결하기 위해 다양한 기법들이 사용되어 왔으나 자바의 한계로 복잡도가 상당히 올라가는 모습을 보인바 있습니다.

허나 코틀린 First의 시대에 접어들면서 코틀린의 확장 함수 기능을 사용하여 손쉽게 로깅하는 유틸을 만들어낼 수 있고 이를 사용하는 방법에 대해 소개합니다.

## BuildConfig를 활용해라

BuildConfig 클래스는 컴파일했을 때 생성됩니다. 사용자가 임의로 생성해주는 클래스는 아니며 임의의 프로퍼티를 `build.gradle`에서 추가할 수 있습니다.

`build.gradle`에 대해 자세히 설명하지는 않겠으나, 핵심은 `android` 블록에서 빌드 단계를 정의할 수 있다는 것이고 기본적으로 `debug`와 `release` 단계가 존재합니다.

이를 토대로 프로젝트를 빌드했을 때 어떤 variant를 선택했느냐에 따라 `BuildConfig` 클래스의 정적 필드 `DEBUG`의 값이 결정됩니다:

- `debug`라면 `true`
- `release`라면 `false`

이를 알고 있다면 로그를 남길 때 다음과 같이 활용할 수 있습니다.

```kotlin
if(BuildConfig.DEBUG) Log.i("Tag", "Debug일 때만 로깅")
```

## 확장 함수를 사용해라

위 예제에서 소개된 코드의 문제점은 로깅하는 문마다 `BuildConfig.DEBUG`의 값이 `true`인지 확인하는 부분입니다.

이는 엄청난 반복 코드를 생산하게 되므로 이를 막기 위해 코틀린의 확장 함수를 활용합니다.

```kotlin
fun Any.info(message: String) {
    if (BuildConfig.DEBUG) Log.i(this::class.simpleName, message)
}
```

```kotlin
class Test {

    fun test() {
        info("testing")
    }
}
```

- `Any`의 확장 함수를 만들게 되면 모든 클래스에서 `info` 함수를 호출할 수 있게됩니다.
- `this::class.simpleName`는 이 함수를 호출한 클래스의 이름을 String으로 받아옵니다. 만약 `Test` 클래스에서 `info()` 함수를 호출했다면 `"Test"` 문자열이 됩니다. 이는 로그를 사용할 때의 가장 불편한 문제인 Tag를 정의하는 문제에서 손쉽게 해결하고, 로깅 메시지에 좀 더 집중할 수 있게 도와줍니다.

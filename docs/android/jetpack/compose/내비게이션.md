# 컴포저블 내비게이션(Navigation)

컴포저블 간의 이동은 내비게이션을 이용해야 합니다.

## 의존성 추가

모듈 단위의 `build.gradle` 파일에 다음 의존성을 추가하세요.

=== "Groovy"

    ```groovy
    dependencies {
        implementation "androidx.navigation:navigation-compose:2.5.3"
    }
    ```

=== "Kotlin"

    ```kotlin
    dependencies {
        implementation("androidx.navigation:navigation-compose:2.5.3")
    }
    ```

## NavController

`NavController`는 컴포저블의 백스택[^1]을 추적합니다.

컴포저블에서 `rememberNavConstoller()` 메서드를 사용하여 `NavController`를 얻을 수 있습니다.

```kotlin
val navController = rememberNavController()
```

???+ notice

    **참고**: `NavController`를 만드는 위치는 이 객체를 참조해야 하는 모든 컴포저블이 접근할 수 있는 위치어야 합니다.

## NavHost

`NavHost`는 내비게이션 그래프[^2]와 `NavController`를 연결합니다.

여러 `NavController`를 단일 NavHost와 연결해야 합니다.

컴포저블 간에 이동하는 과정에서 `NavHost`의 콘텐츠가 자동으로 재구성됩니다. 내비게이션 그래프에 연결된 대상은 각각 경로[^3]와 연결됩니다.

`NavHost`를 만들기 위해 다음 두 가지가 필요합니다:

- 이전에 `rememberNavController()`를 통해 만든 `NavController`
- 그래프의 시작 대상 경로

```kotlin
NavHost(navController = navController, startDestination = "first") {
    composable("first") { FirstScreen(/*...*/) }
    composable("second") { SeceondScreen(/*...*/) }
    /*...*/
}
```

## 컴포저블로 이동

내비게이션 그래프에서 컴포저블로 이동하려면 `navigate` 메서드를 사용해야 합니다. `navigate`는 컴포저블의 경로를 나타내는 문자열 매개변수를 사용합니다.

```kotlin
navController.navigate("seceond")
```

`navigate` 메서드는 새로운 컴포저블을 백스택에 추가합니다. 호출할 때 [옵션](https://developer.android.com/guide/navigation/navigation-navigate#pop)을 추가할 수도 있습니다.

### 옵션: 현재 백스택 지우기

"second"로 이동하기 전에 백 스택에서 "home" 컴포저블까지의 스택을 꺼냅니다(`pop`).

```kotlin
navController.navigate("second") {
    popUpTo("home")
}
```

### 옵션: 백 스택 모두 지우기

"second"로 이동하기 전에 백 스택에서 "home"을 포함한 모든 스택을 꺼냅니다(`pop`).

```kotlin
navController.navigate("second") {
    popUpTo("home") { inclusive = true }
}
```

### 옵션: 백 스택 상단에 복사본 방지

아직 "second"가 있지 않은 경우에만 "second"로 이동하여, 백 스택 상단에 복사본이 생기는 것을 막을 수 있습니다.

```kotlin
navController.navigate("second") {
    launchSingleTop = true
}
```

[^1]:
    백스택이란 사용자의 컴포저블간 이동 히스토리로 생각하면 됩니다. 새로운 컴포저블로 이동했을 때 추가(`push`)하고, 이전으로 돌아갈 때 가져옵니다(`pop`).
[^2]:
    내비게이션 그래프란 각 컴포저블마다 이동할 수 있는 모든 경로를 담고 있는 리소스입니다.
[^3]:
    경로는 컴포저블의 경로를 정의한 문자열입니다. 기존 암시적 인텐트와 역할이 비슷합니다. 모든 컴포저블의 경로는 고유해야 합니다.

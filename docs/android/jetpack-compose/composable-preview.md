---
title: 제트팩 컴포즈 미리보기
description: 컴포저블 함수를 안드로이드 스튜디오에서 에뮬레이터나 물리적인 하드웨어에 의존적이지 않게 UI를 확인해볼 수 있습니다.
comments: true
---

# Composable 미리보기

안드로이드 스튜디오에 Compose를 위한 기능이 몇 가지 있습니다.

Compose는 코드 중심으로 작성되므로 개발할 때 코드/하이브리드(코드+디자인)/디자인 편집기 중에 고를 필요가 없습니다.

과거 뷰와 Compose의 가장 큰 차이는 UI를 랜더링하는 데 View 클래스를 사용하지 않는다는 것입니다. 따라서 에뮬레이터 또는 실제 기기에 의존하지 않고도 실제 UI가 어떻게 그려지게 될지 바로 확인해볼 수 있습니다.

## 의존성 추가

Compose 전용 기능을 사용하기 위해서 모듈 단위의 `build.gradle` 파일에 다음 의존성을 추가합니다.

=== "build.gradle"

    ``` groovy
    dependencies {
        debugImplementation "androidx.compose.ui:ui-tooling:1.3.0"
        implementation "androidx.compose.ui:ui-tooling-preview:1.3.0"
    }

    ```

=== "build.gradle.kts"

    ``` kts
    dependencies {
        debugImplementation("androidx.compose.ui:ui-tooling:1.3.0")
        implementation("androidx.compose.ui:ui-tooling-preview:1.3.0")
    }
    ```

## Composablepreview 적용

텍스트를 출력하는 컴포저블을 정의합니다.

``` kt title="MainActivity.kt"
@Composable
fun SimpleComposable() {
    Text("Hello World")
}
```

이 컴포저블의 미리보기를 사용 설정하려면 `@Preview` 주석이 있는 컴포저블을 추가로 만듭니다.

``` kt title="MainActivity.kt"
@Preview
@Composable
fun ComposablePreview() {
    SimpleComposable()
}
```

마지막으로 스플릿 뷰를 클릭하여 오른쪽 패널을 엽니다. 이 패널에 비리보기가 표시됩니다.

![split view](https://developer.android.com/static/images/jetpack/compose/tooling-split-view.png)
![ComposablePreview](https://developer.android.com/static/images/jetpack/compose/tooling-simple-preview.png)

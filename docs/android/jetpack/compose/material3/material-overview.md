---
title: Material 3 구현
description: 제트팩 컴포즈는 머티리얼 디자인 3 구현을 제공합니다. 머티리얼 3에는 테마, 컴포넌트, 동적 색상과 같은 개인화(Material You) 기능이 포함되어 있으며 안드로이드 12 이상의 UI와 결합되도록 설계되어 있습니다.
comments: true
---

# 머티리얼 3 컴포즈로 구현하기

제트팩 컴포즈를 사용하면 **머티리얼 3** 를 구현할 수 있습니다.

!!! Tip

    "머티리얼 3" 또는 "Material 3"는 앞으로 **M3** 라고 칭합니다.

## 의존성

사용할 모듈 수준의 `build.gradle`파일에 의존성을 추가합니다.

=== "Groovy"

    ```groovy
    def composeBom = platform('androidx.compose:compose-bom:2022.10.00')
    implementation composeBom
    androidTestImplementation composeBom

    implementation 'androidx.compose.material3:material3'
    ```

=== "Kotlin"

    ```Kotlin
    val composeBom = platform("androidx.compose:compose-bom:2022.10.00")
    implementation composeBom
    androidTestImplementation composeBom

    implementation("androidx.compose.material3:material3")
    ```

## M3 `@OptIN`

현재 M3의 일부 API는 실험적인 것으로 간주되어 `@OptIN` 어노테이션을 사용하여 함수(`fun`) 또는 파일 수준에서 동의해야 합니다.

```kotlin
import androidx.compose.material3.ExperimentalMaterial3Api

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun AppComposable() {
    // M3 composables
}
```

## M3 테마

M3 테마는 [color scheme], [typography], [shapes]와 같은 하위 시스템이 포함되어 있습니다. 이 값을 커스텀하면, 앱을 빌드하는 데 사용하는 M3 컴포넌트에 변경 사항이 자동으로 반영됩니다.

  [color scheme]: https://m3.material.io/styles/color/overview
  [typography]: https://m3.material.io/styles/typography/overview
  [shapes]: https://m3.material.io/styles/shape/overview

컴포즈는 M3의 `MaterialTheme` 컴포저블을 사용하여 위 3가지 개념을 구현합니다.

```kotlin
MaterialTheme(
    colorScheme = …,
    typography = …,
    shapes = …
) {
    // M3 app content
}
```

### 색상 구성표

### 서체

### 도형

### 강조

## M3 컴포넌트

M3는 이미 머티리얼 테마를 따르는 컴포넌트가 사전에 구현되어 있습니다:

- Button
- Chip
- Card
- Navigation
- etc

M3는 강조와 관심도에 따라 다른 역할에 사용되는 동일한 컴포넌트를 여러 버전으로 제공합니다.

### 내비게이션 컴포넌트

## 예제

- [Samples](https://cs.android.com/androidx/platform/frameworks/support/+/androidx-main:compose/material3/material3/samples/src/main/java/androidx/compose/material3/samples/)
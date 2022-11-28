---
title: 제트팩 컴포즈 시작하기
description: Jetpack Compose를 시작하기 위해 의존성 관리 방법을 소개합니다.
comments: true
---

# Jetpack Compose 시작하기

!!! warning

    Minimum API level은 **21** 이상이어야 합니다.

## build.gradle (:app) 설정

compose를 사용하는 모듈 수준의 `build.gradle` 파일에 다음과 같은 정의를 추가해야 합니다.

- android>buildFeatures: Compose 활성화
- android>composeOptions: Kotlin 라이브러리 버전 지정
- dependencies: 사용하는 의존성 추가

### android 블록 정의

=== "Groovy"

    ```Groovy
    android {
      buildFeatures {
        compose true
      }

      composeOptions {
        kotlinCompilerExtensionVersion = "1.3.2"
      }
    }
    ```

=== "Kotlin"

    ```Kotlin
    android {
      buildFeatures {
        compose = true
      }

      composeOptions {
        kotlinCompilerExtensionVersion = "1.3.2"
      }
    }
    ```

- `buildFeatures` 블록 내에서 `compose` 플래그를 `true`로 설정하면 `compose` 기능을 활성화합니다.
- `composeOptions` 블록에 정의된 `kotlinCompilerExtensionVersion`는 Kotlin 버전 관리에 연관되어 있습니다. [여기](https://developer.android.com/jetpack/androidx/releases/compose-kotlin?hl=ko){target=_blank}를 참고하여 프로젝트의 Kotlin 버전과 일치하는 버전을 선택해야 합니다.

### dependencies 추가

Compose 라이브러리는 매우 급진적인 라이브러리라 각각의 라이브러리가 같은 버전 넘버링을 사용하지 않습니다.

따라서 호환되는 라이브러리를 미리 세트로 묶어둔 BOM[^1] 사용을 적극 권장합니다.

=== "Groovy"

    ```Groovy
    dependencies {

        def composeBom = platform('androidx.compose:compose-bom:2022.10.00')
        implementation composeBom
        androidTestImplementation composeBom

        // Material 디자인 라이브러리는 2 또는 3 중에 선택
        // Material Design 3 (실험적이라 일부 사용에 OptIn이 필요함)
        implementation 'androidx.compose.material3:material3'
        // 또는 Material Design 2
        implementation 'androidx.compose.material:material'
        // 또는 Material 디자인을 skip하고, 기본 구성요소 위에 직접 빌드
        implementation 'androidx.compose.foundation:foundation'
        // 또는 입력 및 측정/레이아웃과 같은 기본 toolkit 시스템의 기본 API만 import
        implementation 'androidx.compose.ui:ui'

        // 안드로이드 스튜디오의 컴포저블 미리보기
        implementation 'androidx.compose.ui:ui-tooling-preview'
        debugImplementation 'androidx.compose.ui:ui-tooling'

        // UI 테스팅
        androidTestImplementation 'androidx.compose.ui:ui-test-junit4'
        debugImplementation 'androidx.compose.ui:ui-test-manifest'

        // Optional - Included automatically by material, only add when you need
        // the icons but not the material library (e.g. when using Material3 or a
        // custom design system based on Foundation)
        implementation 'androidx.compose.material:material-icons-core'
        // Optional - Add full set of material icons
        implementation 'androidx.compose.material:material-icons-extended'
        // Optional - Add window size utils
        implementation 'androidx.compose.material3:material3-window-size-class'

        // Optional - Integration with activities
        implementation 'androidx.activity:activity-compose:1.5.1'
        // Optional - Integration with ViewModels
        implementation 'androidx.lifecycle:lifecycle-viewmodel-compose:2.5.1'
        // Optional - Integration with LiveData
        implementation 'androidx.compose.runtime:runtime-livedata'
        // Optional - Integration with RxJava
        implementation 'androidx.compose.runtime:runtime-rxjava2'

    }
    ```

=== "Kotlin"

    ```Kotlin
    dependencies {

        val composeBom = platform("androidx.compose:compose-bom:2022.10.00")
        implementation composeBom
        androidTestImplementation composeBom

        // Choose one of the following:
        // Material Design 3
        implementation("androidx.compose.material3:material3")
        // or Material Design 2
        implementation("androidx.compose.material:material")
        // or skip Material Design and build directly on top of foundational components
        implementation("androidx.compose.foundation:foundation")
        // or only import the main APIs for the underlying toolkit systems,
        // such as input and measurement/layout
        implementation("androidx.compose.ui:ui")

        // Android Studio Preview support
        implementation("androidx.compose.ui:ui-tooling-preview")
        debugImplementation("androidx.compose.ui:ui-tooling")

        // UI Tests
        androidTestImplementation("androidx.compose.ui:ui-test-junit4")
        debugImplementation("androidx.compose.ui:ui-test-manifest")

        // Optional - Included automatically by material, only add when you need
        // the icons but not the material library (e.g. when using Material3 or a
        // custom design system based on Foundation)
        implementation("androidx.compose.material:material-icons-core")
        // Optional - Add full set of material icons
        implementation("androidx.compose.material:material-icons-extended")
        // Optional - Add window size utils
        implementation("androidx.compose.material3:material3-window-size-class")

        // Optional - Integration with activities
        implementation("androidx.activity:activity-compose:1.5.1")
        // Optional - Integration with ViewModels
        implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.5.1")
        // Optional - Integration with LiveData
        implementation("androidx.compose.runtime:runtime-livedata")
        // Optional - Integration with RxJava
        implementation("androidx.compose.runtime:runtime-rxjava2")

    }
    ```

[^1]:
    **BOM(Bill of Materials)** 이란 프로젝트의 의존성 버전을 중앙(이 경우 구글)에서 제어하기 위해 사용됩니다.

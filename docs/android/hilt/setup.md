---
title: 의존성 주입 with Hilt
comments: ture
---

객체간 의존성을 관리하는 것은 매우 복잡한 일이기도 하고 수많은 상용구를 남발하게 되는 원인입니다.

Hilt는 프로젝트에 있는 모든 클래스에 컨테이너를 제공하여 수명주기를 자동으로 관리해 애플리케이션에서 DI를 사용할 수 있도록 지원합니다.

Hilt는 기존에 인기리(?)에 사용되던 Dagger를 기반으로 빌드된 라이브러리로 Dagger가 제공하던 컴파일 타임에서의 정확성, 런타임 성능 확보, Android 스튜디오 공식 지원의 이점을 얻을 수 있습니다.

## 1. 의존성 추가

Hilt 라이브러리를 사용하기 위해서 프로젝트 루트에 있는 `build.gradle` 파일에 `hilt-android-gradle-plugin` 플러그인을 추가합니다.

=== "Groovy"

    ```groovy title="build.gradle" hl_lines="3"
    plugins {
        ...
        id 'com.google.dagger.hilt.android' version '2.44' apply false
    }
    ```

=== "Kotlin"

    ``` kotlin title="build.gradle.kts" hl_lines="3"
    plugins {
        ...
        id("com.google.dagger.hilt.android") version "2.44" apply false
    }
    ```

그 다음 적용하고자 하는 모듈의 `build.gragle` 파일에 플러그인 및 종속성을 적용합니다.

=== "Groovy"

    ```groovy title="build.gradle" hl_lines="2 3 9 10 11 12 16 17 21 22 23"
    plugins {
        id 'kotlin-kapt'
        id 'com.google.dagger.hilt.android'
    }

    android {
        ...
        // Hilt는 Java 8 기능을 사용하기 때문에 Java 8을 활성화합니다.
        compileOptions {
            sourceCompatibility JavaVersion.VERSION_1_8
            targetCompatibility JavaVersion.VERSION_1_8
        }
    }

    dependencies {
        implementation "com.google.dagger:hilt-android:2.44"
        kapt "com.google.dagger:hilt-compiler:2.44"
    }

    // Allow references to generated code
    kapt {
        correctErrorTypes true
    }
    ``` 

=== "Kotlin"

    ``` kotlin title="build.gradle.kts" hl_lines="2 3 9 10 11 12 16 17 21 22 23"
    plugins {
        kotlin("kapt")
        id("com.google.dagger.hilt.android")
    }

    android {
        ...
        // Hilt는 Java 8 기능을 사용하기 때문에 Java 8을 활성화합니다.
        compileOptions {
            sourceCompatibility = JavaVersion.VERSION_1_8
            targetCompatibility = JavaVersion.VERSION_1_8
        }
    }

    dependencies {
        implementation("com.google.dagger:hilt-android:2.44")
        kapt("com.google.dagger:hilt-android-compiler:2.44")
    }

    // Allow references to generated code
    kapt {
        correctErrorTypes = true
    }
    ```

!!! note

    **Note**: Hilt와 데이터 바인딩을 모두 사용하는 프로젝트에는 Android Studio 4.0 이상이 필요합니다.

## 2. `@HiltAndroidApp`

Hilt를 포함하는 모든 앱에는 `Application` 클래스를 구현하고 `@HiltAndroidApp` 어노테이션을 추가해야 합니다.

`HiltAndroidApp`은 종속성 컨테이너 역할을 수행하는 Application 클래스의 베이스 클래스를 포함하여 Hilt의 코드 생성을 트리거합니다.

=== "Java"

    ``` java title="ExampleApplication.java" hl_lines="1"
    @HiltAndroidApp
    public class ExampleApplication extends Application { ... }
    ```

=== "Kotlin"

    ``` kotlin title="ExampleApplication.kt" hl_lines="1"
    @HiltAndroidApp
    class ExampleApplication : Application() { ... }
    ```

이렇게 생성된 Hilt 컴포넌트는 `Application` 객체의 생명주기에 포함되어 안드로이드 애플리케이션에게 의존성을 제공합니다. 또한 앱의 최상위 컴포넌트이기에 다른 컴포넌트가 이 `Application` 컴포넌트가 제공하는 의존성에 접근할 수 있습니다.

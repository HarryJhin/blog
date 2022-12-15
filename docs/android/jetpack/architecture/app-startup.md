---
comments: true
---

# App Startup

App Startup 라이브러리는 애플리케이션 시작 시 구성 요소를 초기화하는 간단하고 성능도 챙길 수 있는 방법을 제공합니다. App Startup을 사용하여 초기화 순서를 명시적으로 설정할 수 있습니다.

초기화해야 하는 각 구성 요소에 대해 별도의 콘텐츠 제공자를 정의하는 대신 App Startup을 사용하면 단일 콘텐츠 제공자를 공유하는 구성 요소 초기화 프로그램을 정의할 수 있습니다. 이렇게 하면 앱 시작 시간이 크게 향상 될 수 있습니다.

## Setup

=== "Groovy"

    ```groovy
    dependencies {
      implementation "androidx.startup:startup-runtime:1.1.1"
    }
    ```

=== "Kotlin"

    ```kotlin
    dependencies {
      implementation("androidx.startup:startup-runtime:1.1.1")
    }
    ```

## 구성요소 초기화

특정 케이스에서 앱이 시작될 때 즉시 초기화되는 컴포넌트에 의존합니다.

콘텐츠 제공자를 사용하여 각 종속성을 초기화한다면 위 요구사항을 충족시킬 수 있기는 합니다. 하지만 콘텐츠 제공자는 인스턴스화하는 데 비용이 많이 들고 앱의 시작 시퀀스가 불필요하게 늦춰질 수 있습니다. 또한 안드로이드는 콘텐츠 제공자를 초기화하는 데 순서를 지키지 않습니다.

따라서 App Startup은 앱 시작 시 컴포넌트를 초기화하고 해당 종속성을 명시적으로 정의하는 보다 효율적인 방법을 제공합니다.

App Startup을 사용하여 시작 시 자동으로 컴포넌트를 초기화하려면 앱이 초기화해야 하는 각 컴포넌트에 대해 초기화 프로그램을 정의해야 합니다.

### 컴포넌트 initializers 구현

`Initializer<T>` 인터페이스를 구현하는 클래스를 생성하고 각 컴포넌트 initializer를 정의합니다. 이 인터페이스를 중요한 두 가지 메서드를 정의해야 됩니다

- `create(context: Context)`: 컴포넌트를 초기화하고 `T`의 인스턴스를 반환하는 데 필요한 모든 작업을 포함합니다.
- `dependencies()`: initializer가 의존하는 다른 `Initializer<T>` 객체의 목록을 반환합니다. 이 메서드를 사용하여 앱이 시작할 때 초기화 프로그램을 실행하는 순서를 제어할 수 있게 됩니다.

예를 들어 앱이 WorkManager에 의존하고 시작 시 앱을 초기화해야 한다면, 다음과 같이 구현해볼 수 있습니다.

=== "Java"

    ```java
    // Initializes WorkManager
    class WorkManagerInitializer implements Initializer<WorkManager> {

        @Override
        public WorkManager create(Context context) {
            Configuration configuration = Configuration.Builder().build();
            WorkManager.initialize(context, configuration);
            return WorkManager.getInstance(context);
        }

        @Override
        public List<Class<Initializer<?>>> dependencies() {
            // No dependencies on other libraries.
            return emptyList();
        }

    }
    ```

=== "Kotlin"

    ```kotlin
    // Initializes WorkManager
    class WorkManagerInitializer : Initializer<WorkManager> {
        override fun create(context: Context): WorkManager {
            val configuration = Configuration.Builder().build()
            WorkManager.initialize(context, configuration)
            return WorkManager.getInstance(context)
        }
        override fun dependencies(): List<Class<out Initializer<*>>> {
            // No dependencies on other libraries.
            return emptyList()
        }
    }
    ```

`WorkManager`가 다른 라이브러리에 의존하지 않기 때문에 `dependencies()` 함수에서 빈 리스트를 반환합니다.

만약 `WorkManager`에 종속된 `ExampleLogger`가 있다면, 이 종속성은 `App Startup`이 `WorkManager`를 먼저 초기화하는지 확인해야 합니다. 따라서 다음과 같이 구현됩니다:

=== "Java"

    ```java
    // Initializes ExampleLogger
    class ExampleLoggerInitializer implements Initializer<ExampleLogger> {

        @Override
        public ExampleLogger create(Context context) {
            // WorkManager.getInstance() is non-null only after
            // WorkManager is initialized.
            return ExampleLogger(WorkManager.getInstance(context));
        }

        @Override
        public List<Class<Initializer<?>>> dependencies() {
            // Defines a dependency on WorkManagerInitializer so it can be
            // initialized after WorkManager is initialized.
            return Arrays.asList(WorkManagerInitializer.class);
        }
    }
    ```

=== "Kotlin"

    ```kotlin
    // Initializes ExampleLogger
    class ExampleLoggerInitializer : Initializer<ExampleLogger> {
        override fun create(context: Context): ExampleLogger {
            // WorkManager.getInstance() is non-null only after
            // WorkManager is initialized.
            return ExampleLogger(WorkManager.getInstance(context))
        }

        override fun dependencies(): List<Class<out Initializer<*>>> {
            // Defines a dependency on WorkManagerInitializer so it can be
            // initialized after WorkManager is initialized.
            return listOf(WorkManagerInitializer::class.java)
        }
    }
    ```

`dependencies()` 함수에 `WorkManagerInitializer`를 포함한 리스트를 반환하기 때문에 앱 시작은 `WorkManager`를 `ExampleLogger`보다 먼저 초기화합니다.

!!!warning

    **주의**: 이전에 content providers를 사용하여 앱의 컴포넌트를 초기화한 경우 `App Startup`을 사용할 때 해당 content providers를 제거해야 합니다.

### 매니페스트 항목 설정

`App Startup`에는 컴포넌트 이니셜라이저를 검색하고 호출하는 데 사용하는 `InitializationProvider`라는 특수한 콘텐츠 공급자가 포함되어 있습니다.
`App Startup`은 먼저 `InitializationProvider` 매니페스트 항목 아래의 `<meta-data>` 항목을 확인하여 컴포넌트 이니셜라이저를 검색합니다.
그런 다음 `App Startup`은 이미 발견한 초기화 프로그램에 대해 `dependencies()` 메서드를 호출하여 종속성을 확인합니다.

즉, `App Startup`에서 컴포넌트 이니셜라이저를 검색할 수 있으려면 다음 조건 중 하나를 충족해야 합니다:

- 컴포넌트 이니셜라이저에는 `InitializationProvider` 매니페스트 항목 아래에 해당하는 `<meta-data>` 항목이 있습니다.
- 컴포넌트 이니셜라이저는 이미 검색 가능한 이니셜라이저의 `dependencies()` 함수에 (리스트로) 나열됩니다.

```xml title="AndroidManifest.xml"
<provider
    android:name="androidx.startup.InitializationProvider"
    android:authorities="${applicationId}.androidx-startup"
    android:exported="false"
    tools:node="merge">
        <!-- This entry makes ExampleLoggerInitializer discoverable. -->
        <meta-data  android:name="com.example.ExampleLoggerInitializer"
            android:value="androidx.startup" />
</provider>
```

### lint 체크

`App Startup` 라이브러리에는 컴포넌트 initializers를 올바르게 정의했는지 여부를 확인하는 데 사용할 수 있는 lint rule이 포함되어 있습니다.

명령줄에서 `./gradlew :app:lintDebug`를 실행하여 린트 검사를 수행할 수 있습니다.

## 수동으로 컴포넌트 초기화

일반적으로 `App Startup`을 사용할 때 `InitializationProvider` 객체는 `AppInitializer`라는 엔티티를 사용하여 앱 시작 시 컴포넌트 `initializers`를 자동으로 검색하고 실행합니다.
그러나 시작 시 앱에 필요하지 않은 컴포넌트를 수동으로 초기화하기 위해 `AppInitializer`를 개발자가 직접 사용할 수도 있습니다.

이 행위를 지연 초기화(lazy initialization)라고 하며, 앱의 시작 리소스를 최소화하는 데 도움을 줄 수 있습니다.

수동 초기화를 사용하려면 먼저 사용하려는 컴포넌트의 자동 초기화를 비활성화해야 합니다.

### 컴포넌트 자동 초기화 비활성화

단일 컴포넌트에 대한 자동 초기화를 비활성화하려면 매니페스트에서 해당 컴포넌트의 이니셜라이저에 대한 `<meta-data>` 항목을 제거합니다.

예를 들어, `ExampleLogger`에 대한 자동 초기화를 비활성화하는 방법은 다음과 같습니다:

```xml title="AndroidManifest.xml"
<provider
    android:name="androidx.startup.InitializationProvider"
    android:authorities="${applicationId}.androidx-startup"
    android:exported="false"
    tools:node="merge">
    <meta-data android:name="com.example.ExampleLoggerInitializer"
        tools:node="remove" />
</provider>
```

단순히 항목을 제거하는 대신 항목에서 `toolds:node="remove"`를 사용하여 병합된 다른 모든 매니페스트 파일에서도 해당 항목을 제거하도록 합니다.

!!!warning

    **주의**: 컴포넌트에 대한 자동 초기화를 비활성화하면 해당 컴포넌트의 종속성에 대한 자동 초기화도 비활성화됩니다.

### 모든 컴포넌트 자동 초기화 비활성화

모든 자동 초기화를 비활성화하려면 매니페스트에서 `InitializationProvider`에 대한 전체 항목을 제거합니다.

```xml title="AndroidManifest.xml"
<provider
    android:name="androidx.startup.InitializationProvider"
    android:authorities="${applicationId}.androidx-startup"
    tools:node="remove" />
```

### 수동으로 컴포넌트 initializers 호출

컴포넌트에 대해 자동 초기화가 비활성화된 경우 `AppInitializer`를 사용하여 해당 컴포넌트와 해당 종속성을 수동으로 초기화할 수 있습니다.

예를 들어 수동으로 `ExampleLogger`를 초기화하는 방법입니다:

=== "Java"

    ```java
    AppInitializer.getInstance(context)
        .initializeComponent(ExampleLoggerInitializer.class);
    ```

=== "Kotlin"

    ```kotlin
    AppInitializer.getInstance(context)
        .initializeComponent(ExampleLoggerInitializer::class.java)
    ```

결과적으로 `WorkManager`는 `ExampleLogger`의 종속 항목이므로 `App Startup`도 `WorkManager`를 초기화합니다.
---
title: Hilt로 WorkManager 사용하기
comments: true
---

# Hilt - WorkManager

## 설정

=== "Groovy"

    ```Groovy title="build.gradle"
    dependencies {
        implementation 'androidx.hilt:hilt-work:1.0.0'
        // When using Kotlin.
        kapt 'androidx.hilt:hilt-compiler:1.0.0'
        // When using Java.
        annotationProcessor 'androidx.hilt:hilt-compiler:1.0.0'
    }
    ```

=== "Kotlin"

    ```Kotlin title="build.gradle.kts"
    dependencies {
        implementation("androidx.hilt:hilt-work:1.0.0")
        // When using Kotlin.
        kapt("androidx.hilt:hilt-compiler:1.0.0")
        // When using Java.
        annotationProcessor("androidx.hilt:hilt-compiler:1.0.0")
    }
    ```

## 사용법

`@HiltWorker` 어노테이션과 `Worker` 클래스의 생성자(contructor)에 `@AssistedInject`를 사용하여 `Worker`를 삽입합니다. `Worker` 클래스에는 `@Singleton` 또는 범위가 지저오디지 않은 결합만 사용할 수 있습니다.
또한 다음과 같이 `Context` 및 `WorkerParameters` 파라미터에 `@Assisted` 어노테이션으로 지정해줘야 합니다.

=== "Java"

    ```Java
    @HiltWorker
    public class ExampleWorker extends Worker {

        private final WorkerDependency workerDependency;

        @AssistedInject
        ExampleWorker(
            @Assisted @NonNull Context context,
            @Assisted @NonNull WorkerParameters params,
            WorkerDependency workerDependency
        ) {
            super(context, params);
            this.workerDependency = workerDependency;
        }
    }
    ```

=== "Kotlin"

    ```Kotlin
    @HiltWorker
    class ExampleWorker @AssistedInject constructor(
        @Assisted appContext: Context,
        @Assisted workerParams: WorkerParameters,
        workerDependency: WorkerDependency
    ) : Worker(appContext, workerParams) { ... }
    ```

## 수동 초기화

HiltWorkerFactory를 사용한 Worker 생성을 위해 수동 초기화 작업이 필요합니다.

### 버전 2.6.0-alpha01 이후

버전 2.6부터 `App startup`은 WorkManager는 수동 초기화를 사용해야 합니다. 이를 위해 `androidx.startup` 노드를 삭제해야 합니다.

다음은 매니페스트에서 `WorkManagerInitializer` 노드만 삭제하는 설정입니다:

```xml title="AndroidManifest.xml"
<provider
    android:name="androidx.startup.InitializationProvider"
    android:authorities="${applicationId}.androidx-startup"
    android:exported="false"
    tools:node="merge">
    <!-- If you are using androidx.startup to initialize other components -->
    <meta-data
        android:name="androidx.work.WorkManagerInitializer"
        android:value="androidx.startup"
        tools:node="remove" />
</provider>
```

=== "Java"

    ```Java
    @HiltAndroidApp
    public class ExampleApplication extends Application implements Configuration.Provider {

        @Inject HiltWorkerFactory workerFactory;

        @Override
        public Configuration getWorkManagerConfiguration() {
            return new Configuration.Builder()
            .setWorkerFactory(workerFactory)
            .build();
        }
    }
    ```

=== "Kotlin"

    ```Kotlin
    @HiltAndroidApp
    class ExampleApplication : Application(), Configuration.Provider {

        @Inject lateinit var workerFactory: HiltWorkerFactory

        override fun getWorkManagerConfiguration() =
            Configuration.Builder()
                .setWorkerFactory(workerFactory)
                .build()
    }
    ```


### 버전 2.6.0-alpha01 이전

2.6 이전의 WorkManager 버전을 사용하는 동안에는 `workmanager-init`을 대신 삭제합니다.

```xml title="AndroidManifest.xml"
<provider
    android:name="androidx.work.impl.WorkManagerInitializer"
    android:authorities="${applicationId}.workmanager-init"
    tools:node="remove" />
```

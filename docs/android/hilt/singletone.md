---
title: @Singletone과 Kotlin object 클래스의 차이
comments: true
---

아래와 같이 Retrofit 빌더를 통해 통신 클라이언트를 종속성에 등록하는 코드가 있다.

``` kotlin
import dagger.Module
import dagger.Provides
import dagger.hilt.InstallIn
import dagger.hilt.components.SingletonComponent

@Module
@InstallIn(SingletonComponent::class)
object AppModule {

    @Provides
    fun providesApiService(): ApiService {
        return Retrofit.Builder()
            .baseUrl("https://api.example.com/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()
            .create(ApiService::class.java)
    }
}
```

이렇게 등록된 의존성을 주입받는 NetworkService를 만들어보면 다음과 같다.

``` kotlin
class NetworkService @Inject constructor(
    private val apiService: ApiService
) {
    ...
}

```

여기서 고민할 문제가 한가지 있다.

바로 NetworkService를 어떻게 리포지토리에서 가져오면서도 싱글톤을 유지시킬 수 있을까?

일단 방법은 여러가지가 있다:

1. 생성자 호출
2. 의존성 등록

object 클래스가 생각날 수도 있는데 object 클래스는 싱글톤에 부합하지만 언어 자체의 기능이기 때문에 다음과 같은 차이점이 발생한다:

1. 생성 시점: object 클래스는 런타임에서 자동으로 생성되지만, javax.inject.Singletone은 의존성 주입 때 생성된다.
2. 종속성 주입: object는 언어 자체의 기능이므로 사용자가 직접 호출해야하지만, javax.inject.Singletone은 Hilt와 같은 의존성 주입 프레임워크와 함께 동작할 시 자동으로 주입되는 의존성을 처리할 수 있다.
3. 프레임워크: javax.inject.Singletone를 사용하면 Hilt와 같은 의존성 주입 프레임워크의 도움을 받을 수 있다.

근데 위 문제를 다 제치고도 문제가 있는 데 object 클래스는 생성자를 가질 수 없다. 따라서 필드 주입으로 가야하는데 이 때의 문제는 주입된 필드에 접근할 때 해당 필드가 의존성이 주입이 된 상태인지 보장되지 않는 부분이다. 이 때문에 아직 초기화되지 않았다는 예외를 발생시킬 수 있다.

### 1. 생성자 호출

NetworkService를 호출하는 곳에서 생성자에 필요한 인스턴스를 직접 생성하거나, 의존성 주입으로 받아와서 해결하는 방법이 있다.

전자의 경우, 사용하는 곳마다 인스턴스를 생성해야 하니 싱글톤을 어기게 된다.

후자의 경우, 생성자에 필요한 인스턴스는 싱글톤이 유지되겠지만 생성된 NetworkService 인스턴스는 사용처마다 생성하게 되니 이 역시 싱글톤을 유지할 수 없다.

따라서 적합한 해결 방법은 아니다.

물론, 내부적으로 static 프로퍼티에 자기 자신의 instance를 관리하는 방법을 사용할 수는 있으나 그거 할 시간에 의존성 등록하는 것이 더 효율적이다.

### 2. 의존성 등록

ApiService 의존성을 등록했던 것과 마찬가지로 진행하면 된다.

``` kotlin
import javax.inject.Singletone

@Singletone
class NetworkService @Inject constructor(
    private val apiService: ApiService
) {
    ...
}

```

``` kotlin
import dagger.Module
import dagger.Provides
import dagger.hilt.InstallIn
import dagger.hilt.components.SingletonComponent

@Module
@InstallIn(SingletonComponent::class)
object AppModule {

    @Provides
    fun providesApiService(): ApiService {
        return Retrofit.Builder()
            .baseUrl("https://api.example.com/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()
            .create(ApiService::class.java)
    }

    @Provides
    fun providesNetworkService(
        apiService: ApiService
    ): NetworkService {
        return NetworkService(apiService)
    }
}

```

이렇게 의존성 등록을 해주면 NetworkService는 Hilt가 의존성 주입시 싱글톤을 보장해준다.

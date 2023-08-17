---
comments: true
---

# 타입 추론 (inferred)

코틀린은 타입 추론이 가능한 언어이다.

```kotlin
val a = 10 // (1)
val b: Int = 10
a += b // (2)
```

- (1): 변수 a는 Int(int) 타입
- (2): 변수 a는 Int 타입으로 추론되었기 때문에 `+=` 연산이 가능

사실 요근래 대부분의 언어는 타입 추론이 기본적으로 있기 때문에 신기한 것은 아니지만, Java(JDK 11 이전)와 같은 과거의 언어들은 무조건 타입을 선언해야만 했다.

## 타입 추론의 장단점

위 사례에서 살펴본 것처럼 타입 추론은 개발하는데 매우 유용한 기술이다.

그러나 타입 추론이 모든 상황에서 옳은 것은 아니다.

그 사례를 살펴보자.

### 장점

타입 추론의 장점은 뭐니뭐니해도 변수 선언이 편리해진다는 것이다.

개발을 하면서 변수를 선언하는 것은 사람이 숨을 쉬는 것처럼 매우 당연하면서도 기초적인 작업이다.

만약 이 변수를 선언할 때 무조건 타입을 지정해야 한다면 작업하는데 얼마나 불편해지겠는가.

따라서 생산 효율성을 위해서라도 타입 추론은 필수불가결이다.

그것뿐만 아니라 불필요하게 많은 정보를 표현하여 코드의 길이가 길어지는 것을 막아주기도 한다.

```kotlin
val a = 10
```

`a` 변수를 보면 `10`이라는 값이 할당되었는데 이를 보고 `Int`가 아닌 다른 타입으로 오해할 사람은 없다. 그렇기 때문에 대부분의 상황에서 타입을 생략하는 것은 문제가 되지 않는다.

따라서, 코드 가독성을 위해서라도 타입 추론은 매우 유용한 기술이다.

### 단점

타입 추론은 대부분의 상황에서 옳지만, 그렇기에 아닌 상황도 있다.

바로 상속 구조를 가진 타입을 활용할 경우 자주 맞이하는 문제가 있다.

```kotlin
interface Factory

class SamsungFactory : Factory {
    fun test1() { ... }
}

class AppleFactory : Factory {
    fun test2() { ... }
}
```

위 코드에서는 공장 인터페이스를 두고 구현제 `SamsungFactory`와 `AppleFactory`가 있다.

이름만 봐도 해당 공장들이 무엇을 생산할지 감이 오지 않는가?

밑에서 확인해보자.

```kotlin
interface Phone {
    fun factory(): Factory
}

class Galaxy : Phone {
    override fun factory() = SamsungFactory()
}

class IPhone : Phone {
    override fun factory() = AppleFactory()
}
```

`Phone` 인터페이스의 구현체 `Galaxy`와 `IPhone`이 있다.

`Phone` 인터페이스를 상속받았기 때문에 `factory()` 함수를 구현하여 각자의 공장(`Factory`)를 가지고 있다.

이 때 `factory()` 함수는 `Factory` 타입을 반환하도록 선언되어 있기 때문에 `Phone`의 구현체에서 `Factory`의 구현체인 `SamsungFactory`와 `AppleFactory`를 반환하도록 할 수 있었다.

현재 `Phone` 구현체는 타입 추론으로 반환하는 상태이기에 다음과 같은 코드는 성립한다.

```kotlin
val galaxy = Galaxy()
galaxy.factory().test1()

val iPhone = IPhone()
iPhone.factory().test2()
```

그런데 만약 반환 타입을 Super Type(이 경우 `Factory`)으로 명시했을 경우 어떻게 되는지 보자.

```kotlin
class Galaxy : Phone {
    override fun factory(): Factory = SamsungFactory()
}

class IPhone : Phone {
    override fun factory(): Factory = AppleFactory()
}

val galaxy = Galaxy()
galaxy.factory().test1() // test1() 함수 호출 불가능

val iPhone = IPhone()
iPhone.factory().test2() // test2() 함수 호출 불가능
```

단지 Super Type으로 반환 타입을 명시했을 뿐인데 왜 아까와 다르게 test1, test2 함수를 사용할 수 없었을까?

그 이유는 `Factory` 타입에서는 해당 함수가 존재하지 않기 때문이다.

상속에 대해 공부했다면 알겠지만 부모-자식의 관계에서 자식에만 존재하는 것은 부모가 알 수 없다. 이러한 점 때문에 어쩌면 당연하게도 test1(), test2() 함수는 호출할 수 없었던 것이다.

따라서 아무리 타입 추론이 되는 언어라도 **반환(return)할 때는 타입을 명시** 하는 것이 좋다.

## 결론

**반환(return)할 때는 타입을 꼭 명시** 하도록 하자.

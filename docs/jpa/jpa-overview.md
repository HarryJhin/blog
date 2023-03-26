---
comments: true
---

# JPA

JPA(Java Persistence API)는 Java에서 사용할 수 있는 ORM[^1] 기술의 표준입니다.

[^1]: **ORM**(Object Relational Mapping)이란 Java의 설계와 DB의 설계가 동일하지 않기 때문에 서로가 각각 설계하고, 이 격차를 **ORM 프레임워크가 중계** 해주는 기술입니다.

## JPA를 사용하는 목적

JPA는 인터페이스의 모음입니다.

JPA 표준 명세를 구현한 구현체를 여러가지가 있지만, 가장 대중적인 것은 하이버네이트입니다. (하이버네이트 태생이니 뭐...)

서버 앱 개발자는 SQL을 잘 알고 있어야합니다.

그래야 비즈니스 로직에서 원하는 데이터를 정확하고 빠르게 동작하여 최적화된 성능을 보장받을 수 있기 때문이죠.

그런데, 객체지향적인 Java에서 절차지향적인 SQL을 그대로 쓴다는 것은 Java의 핵심 패러다임을 부정하는 것과 마찬가지입니다.

그래서 이 문제를 해결하기 위해 다양한 시도와 솔루션들이 있어왔으나, 현재에 들어서 사용되는 것이 JPA입니다.

## JPA의 동작 과정

JPA는 내부적으로 JDBC[^2]를 사용하고 있습니다. 즉, JDBC를 사용하기 쉽게 추상화한 기술을 JPA라고 말할 수 있습니다.

[^2]: **JDBC**(Java Database Connectivity)는 **Java에서 데이터베이스에 연결하여 쿼리를 실행** 할 수 있는 방법을 제공하는 Java API 입니다.

사실 JPA는 원래 하이버네이트(오픈소스)에서 유래된 것으로 둘이 사실상 동일하다고 보면 됩니다.

## JPA 사용법

JPA를 사용한 CRUD는 다음과 같이 사용합니다:

```kotlin
jpa.persist(entity) // 생성
jpa.find(entity.id) // 조회
entity.name("변경할 이름") // 수정
jpa.remove(entity) // 삭제
```

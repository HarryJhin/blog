---
comments: true
---

# 영속성 컨텍스트

영속성 컨텍스트(Persistence Context)는 JPA를 이해하기 위해서 알아야할 기초 용어로, 엔티티를 영구 저장하는 환경이라는 의미를 가지고 있습니다.

```java
EntityManager.persist(entity)
```

## 1. 목적

영속성 컨텍스트는 EntityManager가 관리하며 1:1 관계입니다.

이것을 사용하는 이유는 당연히 장점이 있기에 그렇습니다:

- 1차 캐시
- 동일성 보장
- 트랜잭션을 지원하는 쓰기 지연
- 변경 감지(Dirty Checking)
- 지연 로딩(Lazy Loading)

사실 우리가 영속성 컨텍스트라고 부르는 것은 1차 캐시를 말하는 것과 동일합니다.

1차 캐시에 있는 엔티티를 조회하면 실제 쿼리를 작동시키지 않고 바로 반환해준다는 것이 장점이나, 트랜잭션 안에서만 유효하다는 한계 때문에 트랜잭션이 동작하는 아주 한정적인 공간에서만 공유되고 그 외에는 이점을 전혀 누릴 수 없습니다.

!!! Tip

    스프링 등에서 공유되는 영속성 컨텍스트는 1차 캐시가 아닌 2차 캐시를 얘기합니다.


### 1.1. 생명주기

관리되는 대상은 엔티티이며, 관리되는 생명주기는 다음과 같습니다:

| 상태                  | 설명                                           |
| --------------------- | ---------------------------------------------- |
| 비영속(new/transient) | 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태 |
| 영속(managed)         | 영속성 컨텍스트에 관리되는 상태                |
| 준영속(detached)      | 영속성 컨텍스트에 저장되었다가 분리되는 상태   |
| 삭제(removed)         | 삭제된 상태                                    |

## 방법

```java
// 비영속
Entity entity = new Entity();
entity.setId(1L);
entity.setCreatedAt(LocalDateTime.now());

tx.getTransaction().begin(); // EntityManager의 트랜잭션 시작

// 영속
em.persist(entity); // 엔티티를 저장 -> 실제 DB에는 아직 저장되지 않음

// 준영속
em.detached(entity)

// 삭제
em.removed(entity)

tx.commit(); // 트랜잭션 종료 -> 실제로 DB에 저장되는 시점
```

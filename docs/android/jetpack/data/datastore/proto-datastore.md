---
comments: true
---

# Proto Datastore

## 1. 소개

Datastore는 개선된 신규 데이터 저장소 솔루션으로, SharedPreferences를 대체합니다.

Kotlin 코루틴과 Flow를 기반으로 한 Datastore는 타입 객체를 저장하는 Proto Datastore(프로토콜 버퍼로 지원됨) 및 키-값 쌍을 저장하는 Preferences Datastore를 제공합니다.

비동기적이고 일관된 트랜잭션 방식으로 데이터를 저장하여 SharedPreferences의 일부 단점을 해결합니다.


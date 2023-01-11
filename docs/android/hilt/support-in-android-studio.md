---
title: Hilt Navigation Support in Android Studio
description: >-
    Hilt를 사용하면 안드로이드 스튜디오에서 DI 탐색 지원을 받을 수 있습니다.
comments: true
---

# Hilt - 안드로이드 스튜디오 지원

Hilt를 사용하면 필연적으로 생기는 문제점이 하나 있습니다.

바로 생성자에 `@Inject`가 붙어있는 클래스의 DI를 분석할 때입니다.

---
title: "Material Components"
description: "머티리얼 구성요소는 UI를 만들기 위한 구성요소입니다."
comments: true
---

# Material 구성요소 알아보기

Material 구성요소는 `MaterialTheme`에서 제공하는 값을 사용합니다.

```Kotlin
@Composable
fun MyApp() {
    MaterialTheme {
        // 버튼, 카드, 스위치 등과 같은 머티리얼 구성요소들
    }
}
```

## Scaffold

Compose는 머티리얼 컴포넌트를 패턴화한 레이아웃을 제공합니다.

`Scaffold`와 같은 컴포저블은 다양한 컴포넌트와 화면 위젯을 제공합니다.

### 화면 콘텐츠


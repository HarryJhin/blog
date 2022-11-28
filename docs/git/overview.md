---
title: Git - Overview
description: >-
    버전 관리에 대한 중요성과 이를 위해 사용하는 Git에 대해 설명합니다.
comments: true
---

# 왜 Git인가?

버전 관리를 쉽게 할 수 있도록 도와주어 협업, 배포 과정을 손쉽게 해줍니다.

## 버전 관리

우선 Git에 앞서 "버전 관리" 개념에 대해 알아야 합니다.

우리는 어떠한 작업을 하면 시간의 흐름에 따라 작업 내용은 다양할 것입니다.

예를 들어, `antifragile.txt` 파일에 다음과 같이 작성했다고 가정합니다.

```txt title="antifragile.txt"
Anti-ti-ti-ti-fragile, fragile
```

3시간 후에는 다음과 같이 작성했습니다.

```txt title="antifragile.txt"
Anti-ti-ti-ti-fragile, fragile
Anti-ti-ti-ti-fragile
Anti-ti-ti-ti-fragile, fragile
Anti(fragile), anti(fragile)
가시밭길 위로 riding, you made me boost up (ah-ah-ah-ah)
```

그런데 3시간 전으로 돌아가야되는 사정이 생겼습니다.

그러면 수동으로 기억에 의존하여 필요하지 않은 부분을 지워나갈 것입니다.

만약 Office365 제품과 같이 상업 소프트웨어를 사용한다면 자체적인 버전기록 시스템 덕에 손쉽게 이전으로 되돌릴 수 있기는 합니다. 하지만 개발자가 작성하는 파일(`.java`, `.cpp`, `.py`)은 자동으로 버전 기록을 해주지는 않습니다.

따라서 개발자가 원하는 시점에 원하는 내용이 버전이 되어 기록해줄 수 있는 버전 관리 시스템이 필요해졌습니다.

많은 솔루션이 있었으나 결국 선택받은 것은 Git입니다.

현재 대부분의 프로젝트는 버전 관리 도구로 Git을 사용합니다.

## Git 배경

오픈소스 프로젝트 중 가장 큰 Linux 커널 프로젝트는 과거 압축파일로 관리하다 2002년 BitKeeper라는 상용 DVCS를 사용합니다.

2005년 BitKeeper의 무료 사용이 취소되면서 Linux의 이념과 틀어졌고 이에 반발한 라누스 토발즈가 자체 도구 Git을 만들게 되었습니다.

---
comments: true
---

# 스테이지 취소하기

워킹 트리(working tree)의 변경 사항을 스테이지(stage)에 추가(add)했을 때, 버전에 포함하고 싶지 않다는 등의 사유로 스테이지를 취소하고 싶을 때가 있습니다.

이 때 사용할 수 있는 방법은 `reset` 명령입니다.

## 사용법

만약 test.txt 파일의 변경 사항을 스테이지한 상황에서 취소하려면 다음과 같이 입력하면 됩니다.

```bash
git reset HEAD test.txt
```

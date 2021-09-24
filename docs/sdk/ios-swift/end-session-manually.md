---
layout: default
title:  수동 세션 종료
parent: iOS-Swift
grand_parent: SDK
nav_order: 10
---

# 수동 세션 종료

세션을 종료할 때 uploadData 파라미터 세션을 이용해 세션 데이터를 서버로 전송하고 종료할 것인지 선택할 수 있습니다. 서버에 전송하지 않고 종료할 경우, 다음 세션이 시작될 때 세션 데이터를 보냅니다.

```swift
UserHabit.sessionClose(withUploadData: true) {
    print("force exit")
    exit(0);
}
```
---
layout: default
title: 세션 종료시간 설정하기
parent: Android SDK
grand_parent: SDK
nav_order: 4
has_toc: false
---
# 세션 종료시간 설정하기

유저해빗에서는 앱이 백그라운드로 이동한 후 일정 시간 동안 앱을 활성화하지 않을 경우 세션을 종료합니다. 
세션 종료 시간으로 지정된 기본값은 **10초**로 설정되어 있습니다. 해당 값은 아래와 같은 방법으로 수정이 가능합니다.

```java
public class YourApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        Userhabit.setSessionEndTime(10);
        Userhabit.start(this);
  }
}
```
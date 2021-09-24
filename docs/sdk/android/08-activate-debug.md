---
layout: default
title: 디버그 모드 활성화 하기
parent: Android SDK
grand_parent: SDK
nav_order: 8
has_toc: false
---
# 디버그 모드 활성화 하기

디버그 모드를 활성화 하면 유저해빗 수집 과정에 대한 로그 및 스크린샷 수집 모드를 활용 하실 수 있습니다. 

스크린샷 수집 모드는 현재 베타 서비스 중이며, Production 모드에서는 활성화 되지 않습니다. 자세한 내용은 👉🏻 [스크린샷 취득하기](/docs/sdk/android/09-get-screenshot.html) 에서 '수동 스크린샷 수집 모드'를 확인하세요. 

```java
public class YourApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        Userhabit.setDebug(true); 
        Userhabit.start(this);
  }
}
```
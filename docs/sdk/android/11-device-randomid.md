---
layout: default
title: 디바이스 구분자 랜덤 생성 기능
parent: Android SDK
grand_parent: SDK
nav_order: 11
has_toc: false
---
# 디바이스 구분자 랜덤 생성 기능

유저해빗에서는 각각의 디바이스를 구분하기 위하여 Android에서 제공하는`ANDROID_ID`값을 사용합니다. 해당`ANDROID_ID`사용에 관하여 정책에 따라 해당 값을 수집하지 않기 위해서 아래와 같은 함수를 통해서 임의로 지정된 값으로 대체 가능합니다.

```java
public class YourApplication extends Application {
    @Override
    public void onCreate() {
       super.onCreate();
       Userhabit.enableDeviceRandomID(); 
       Userhabit.start(this); 
  }
}
```
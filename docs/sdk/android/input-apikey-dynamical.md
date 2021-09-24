---
layout: default
title:  동적으로 API 키 입력하기
parent: Android SDK
grand_parent: SDK
nav_order: 6
has_toc: false
---

# 동적으로 API 키 입력하기

start 함수에 API 키를 입력할 수 있습니다. 

> **주의!**
AndroidManifest.xml에 API 키가 입력되어 있어도, 동적으로 입력된 API 키를 더 우선으로 합니다.

```java
public class YourApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        Userhabit.start(this, "API KEY");
  }
}
```
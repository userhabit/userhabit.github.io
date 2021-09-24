---
layout: default
title: 사용자 터치 수집 제외하기
parent: Android SDK
grand_parent: SDK
nav_order: 7
has_toc: false
---
# 사용자 터치 수집 제외하기

## 1. **특정 View 영역 제외**

보안상의 이유로 특정 view 영역에 대한 터치를 수집하고 싶지 않다면 아래와 같이 등록하세요.

```java
@Override
public void onStart() {
   super.onStart();
   Userhabit.addSecretView(button1);
}
```

## 2. **특정 시점 제외**

보안상의 이유로 특정 시점에 대하여 터치를 수집하고 싶지 않다면 아래와 같이 등록하세요.

```java
@Override
protected void onResume() {
    super.onResume();
    Userhabit.secretMode(true); //터치 수집 비활성화
}
```

```java
@Override
protected void onPause() {
super.onPause();
Userhabit.secretMode(false); //터치 수집 기능 활성화
}
```
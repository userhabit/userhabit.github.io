---
layout: default
nav_order: 2
title:  Android SDK
parent: SDK
has_children: true
---

# Android SDK 가이드v2

아래 library 를 다운로드 받고 설치해서 사용하면 됩니다. 자세한 내용은 *[SDK 적용하기](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/SDK%20%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%207bbdea6a1b84444a94079d421255922e.md)* 를 참고 하면 됩니다.

**[Android SDK 다운로드](https://s3-ap-northeast-1.amazonaws.com/userhabit-production/sdks/userhabitsdk_1.3.0.aar)(1.3.0, latest version / android support library 사용)**

⚠️ **유저해빗 적용을 위한 최소 요구사항**

- API level 14 이상
- Android support library v4 22.2이상
- Android support recyclerview-v7 등록

Android support library 를 사용할 수 없는 경우에는, `gradle.properties` 파일에 아래설정을 추가해 주면 됩니다.(`com.android.tools.build:gradle:7.0.2` 기준)

- [AndroidX로 이전 | Android 개발자 | Android Developers](https://developer.android.com/jetpack/androidx/migrate#migrate_an_existing_project_using_android_studio)

```groovy
# gradle.properties
...
android.useAndroidX=true
android.enableJetifier=true
```

---

🙋🏻‍♂️ 더 궁금한 사항이 있으면 [문의하기](http://userhabit.io/contact_us)를 클릭해주세요.

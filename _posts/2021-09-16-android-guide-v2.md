---
layout: post
title:  "Android SDK 가이드v2"
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

### 가이드 목차

[SDK 적용하기](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/SDK%20%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%207bbdea6a1b84444a94079d421255922e.md)

[추가 화면 구성하기](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%8E%E1%85%AE%E1%84%80%E1%85%A1%20%E1%84%92%E1%85%AA%E1%84%86%E1%85%A7%E1%86%AB%20%E1%84%80%E1%85%AE%E1%84%89%E1%85%A5%E1%86%BC%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20ac299807a357464b82f3d2f808eeb2a6.md)

[[스크롤 데이터 추적하기](http://userhabit.io/ko/documentations/sdk_android#g_android_scroll_data)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%A9%E1%86%AF%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8E%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%205e3d3c805ff94082bd7046997e8fc25d.md)

[[세션 종료시간 설정하기](http://userhabit.io/ko/documentations/sdk_android#g_android_quit_time)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%89%E1%85%A6%E1%84%89%E1%85%A7%E1%86%AB%20%E1%84%8C%E1%85%A9%E1%86%BC%E1%84%85%E1%85%AD%E1%84%89%E1%85%B5%E1%84%80%E1%85%A1%E1%86%AB%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20e13448c561334a46a0a4b36be6100e55.md)

[[웹뷰 오브젝트 추적하기](http://userhabit.io/ko/documentations/sdk_android#g_android_tracking_webview) (BETA)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%8B%E1%85%B0%E1%86%B8%E1%84%87%E1%85%B2%20%E1%84%8B%E1%85%A9%E1%84%87%E1%85%B3%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B3%20%E1%84%8E%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20(BETA)%205d2cffbec629409190de436f19efe8cb.md)

[[동적으로 API 키 입력하기](http://userhabit.io/ko/documentations/sdk_android#g_android_api)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%8B%E1%85%B3%E1%84%85%E1%85%A9%20API%20%E1%84%8F%E1%85%B5%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%85%E1%85%A7%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20331fc31de56047adab7669bb41cf6ca6.md)

[[사용자 터치 수집 제외하기](http://userhabit.io/ko/documentations/sdk_android#g_android_touch)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%8C%E1%85%A1%20%E1%84%90%E1%85%A5%E1%84%8E%E1%85%B5%20%E1%84%89%E1%85%AE%E1%84%8C%E1%85%B5%E1%86%B8%20%E1%84%8C%E1%85%A6%E1%84%8B%E1%85%AC%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20732e79221db14514a2415efd900986da.md)

[[디버그 모드 활성화 하기](http://userhabit.io/ko/documentations/sdk_android#g_android_debug)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%83%E1%85%B5%E1%84%87%E1%85%A5%E1%84%80%E1%85%B3%20%E1%84%86%E1%85%A9%E1%84%83%E1%85%B3%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%89%E1%85%A5%E1%86%BC%E1%84%92%E1%85%AA%20%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20f75a18345d124261b4e3d70fb1c72fe9.md)

[[스크린샷 취득하기](http://userhabit.io/ko/documentations/sdk_android#g_android_screen)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%20%E1%84%8E%E1%85%B1%E1%84%83%E1%85%B3%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%2079eac99258e345e5abcb36755458c812.md)

[[유입 경로 추적하기](http://userhabit.io/ko/documentations/sdk_android#g_android_tracing)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%8B%E1%85%B2%E1%84%8B%E1%85%B5%E1%86%B8%20%E1%84%80%E1%85%A7%E1%86%BC%E1%84%85%E1%85%A9%20%E1%84%8E%E1%85%AE%E1%84%8C%E1%85%A5%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20815cae55b13a4d34ad02f48853b92c7f.md)

[[디바이스 구분자 랜덤 생성 기능](http://userhabit.io/ko/documentations/sdk_android#g_android_rd_device)](Android%20SDK%20%E1%84%80%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3v2%206d5cbc87ebc545a5836e1f16d4200112/%E1%84%83%E1%85%B5%E1%84%87%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%80%E1%85%AE%E1%84%87%E1%85%AE%E1%86%AB%E1%84%8C%E1%85%A1%20%E1%84%85%E1%85%A2%E1%86%AB%E1%84%83%E1%85%A5%E1%86%B7%20%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%80%E1%85%B5%E1%84%82%E1%85%B3%E1%86%BC%20cba22e0243ce48fcbe6942ffd7deb9f1.md)

---

🙋🏻‍♂️ 더 궁금한 사항이 있으면 [문의하기](http://userhabit.io/contact_us)를 클릭해주세요.

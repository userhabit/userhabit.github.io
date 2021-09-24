---
layout: default
title:  SDK 적용하기
parent: Android SDK
grand_parent: SDK
nav_order: 1
has_toc: false
---

# SDK 적용하기

## 절차

1. 라이브러리 추가하기
2. AndroidManifest.xml 에 설정 추가
3. 코드에 *Userhabit.start* 추가하기
4. 프로가드(Proguard)에 예외추가 하기
5. 확인
    1. SDK가 제대로 적용됐는지 확인
    2. 수집된 data 전송여부 확인

## 1. **라이브러리 추가하기**

라이브러리(library) 를 추가하는 방식은 다음 2가지가 있습니다.

1. **직접 library file을 donwload** 하는 방식
2. **maven repository 이용** 방식: 현재 지원하지 않습니다.

각 방식을 사용하는 방법은 다음과 같습니다.*(메뉴 왼쪽의 ▶︎버튼을 누르면 메뉴가 펼쳐집니다.)*

- **Download 방식**
    1. [링크](https://s3-ap-northeast-1.amazonaws.com/userhabit-production/sdks/userhabitsdk_1.3.0.aar)를 클릭해 안드로이드용 유저해빗 SDK를 다운로드 하세요.
    2. 해당 jar파일을 안드로이드 프로젝트 폴더 밑 libs 추가합니다. (app/libs/)
    3. *app/build.gradle* 의 *dependencies* 에 `implementation files('libs/userhabitsdk_1.3.0.aar')` 추가

    ```groovy
    // app/build.gradle
    plugins {
        ...
    }

    repositories {
    }

    android {
        ...
    }

    dependencies {
        implementation files('libs/userhabitsdk_1.3.0.aar')
        ...
    }
    ```

- **~~maven repository를 이용하는 방식~~**
    1. app/build.gradle에 적용하세요. 아래 소스와 같이 maven주소와 SDK를 추가합니다.

    ```groovy
    repositories {
    	maven { url 'https://repo.userhabit.io/content/groups/public'}
    }

    android { 
    	dependencies { 
    			implementation 'io.userhabit.service:userhabitsdk:1.3.0@aar'
    	}
    }
    ```

## 2. **AndroidManifest.xml 에 설정 추가하기**

아래 5개를 `AndroidManifest.xml` 에 추가해주면 된다.

1. **인터넷 권한** :
    - `<uses-permission android:name="android.permission.INTERNET"/>`
2. **네트워크 상태 체크 권한** :
    - `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>`
3. **targetSdk 가 28이상인 경우** 추가 :
    - targetSdk 28+ Apache Client Registration for UserhabitSDK : `<uses-library android:name="org.apache.http.legacy" android:required="false" />`
    - ⚠️ 적용할 프로젝트가 target SDK 28+일 경우, 안드로이드 9.0(Pie)정책에 의해 Apache HTTP 클라이언트 권한이 반드시 필요합니다.
4. **site(**[userhabit.io](http://userhabit.io/))**에서 발급받은 API KEY 추가** :
    - 발급받은 key 가 `dev_xxxxxxxxxxxxxxxxxx` 라고 하면,
    - `<meta-data android:name="userhabitApiKey" android:value="dev_xxxxxxxxxxxxxxxxxx" />`
5. **유저해빗 서비스 등록** : 
    - `<service android:name="io.userhabit.service.main.service.UserhabitService" />`

```java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
  package="io.userhabit.myapplication2.app" >

  <!--인터넷 권한 추가-->
  <uses-permission android:name="android.permission.INTERNET"/>
  <!--네트워크 상태 체크 권한 추가-->
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

  <application
			android:name=".YourApplication" //application 등록
      android:icon="@mipmap/ic_launcher"
      android:label="@string/app_name"
      android:theme="@style/AppTheme" >

			<!-- targetSDK 28+ Apache Client Registration for UserhabitSDK-->
      <uses-library
           android:name="org.apache.http.legacy"
           android:required="false" />
      
      <!--해당하는 API KEY 발급 받기-->
      <meta-data android:name="userhabitApiKey" android:value="dev_xxxxxxxxxxxxxxxxxx" />

      <!--유저해빗 서비스 등록하기-->
      <service android:name="io.userhabit.service.main.service.UserhabitService" />
  </application>
</manifest>
```

## 3. **소스 코드 추가하기**

아래와 같이 지정된 Application 클래스 내부에 유저해빗 함수를 적용합니다. 
(API 9 지원 프로젝트에 아래 방법을 도입하면 API 14 이상 기기만 데이터를 수집합니다.)

```java
public class YourApplication extends Application {
    public void onCreate() {
        super.onCreate(); 
        Userhabit.start(this);
  }
}
```

**Application class 추가 방법**

Application class 를 사용하지 않는 경우는 Application class를 추가한 후 `Userhabit.start(this)` 코드를 넣으면 됩니다. 

- [Application class 를 추가하는 방법](https://docs.rudderstack.com/stream-sources/rudderstack-sdk-integration-guides/rudderstack-android-sdk/add-an-application-class-to-you-android-application)

## 4. 프로가드(ProGuard) 적용하기

프로가드를 사용하실 경우 아래와 같이 예외 처리 코드를 추가해주세요.

- v4, v7

```java
-dontwarn org.apache.http.**
-dontwarn android.support.**
-dontwarn android.webkit.WebViewClient
-keep class org.apache.** { *; }
-keep interface org.apache.http.** { *; }
-keepnames interface android.support.v4.** { *; }
-keepnames class android.support.v4.** { *; }
-keepnames class android.support.v7.** { *; }
-keepnames interface android.support.v7.** { *; }
```

- 안드로이드 X

```java
-dontwarn org.apache.http.**
-dontwarn android.support.**
-dontwarn android.webkit.WebViewClient
-dontwarn androidx.**
-keep class org.apache.** { *; }
-keep interface org.apache.http.** { *; }
-keep class androidx.** { *; }
-keep interface androidx.** { *; }
```

유저해빗에서는 Android Support 라이브러리로 부터 아래의 클래스를 사용 합니다.

- v4.view.ViewPager
- v4.view.ViewCompat
- v4.widget.DrawerLayout
- v7.widget.RecyclerView

### 5. 확인

**SDK가 제대로 적용됐는지 확인**

정상적으로 실행되면, logcat 에서 아래와 같은 로그가 보인다.

> **주의!**
`Userhabit.setDebug(true)` 코드가 들어가 있어야 아래와 같은 log를 확인할 수 있다.

```
...
2021-09-07 03:14:56.178 5337-5337/com.test.myapplication I/Userhabit: rrr : true
2021-09-07 03:14:56.241 5337-5337/com.test.myapplication I/Userhabit: rrr : true
2021-09-07 03:14:56.253 5337-5337/com.test.myapplication D/UserhabitLog: sdk process success
2021-09-07 03:14:56.255 5337-5337/com.test.myapplication D/UserhabitLog: SESSION => Start (4)
2021-09-07 03:14:56.313 5337-5362/com.test.myapplication D/UserhabitLog: SCREEN_CHANGE => com.test.myapplication.MainActivity::$PORTRAIT$
2021-09-07 03:14:56.642 5337-5364/com.test.myapplication D/UserhabitLog: NETWORK => Session open succeeded
2021-09-07 03:14:56.973 5337-5364/com.test.myapplication D/UserhabitLog: NETWORK => download fail : 403
```

**수집된 data 전송여부 확인**

app 을 종료한 시점에 수집한 data 를 서버로 전송하게 된다. 아래처럼 logcat 에서 data 를 전송했다는 log를 확인할 수 있다. 

log에서도 보이듯이, app이 background 로 넘어간 후, 일정시간이 지나야 app 이 종료됐다고 인식해서 data 를 전송한다.

- 세션 종료시간 설정 메뉴얼: [https://userhabit.notion.site/58ae0692a267462c8c85165f05b7ebb6](/docs/sdk/android/session-endtime.html)

> **주의!**
`Userhabit.setDebug(true)` 코드가 들어가 있어야 아래와 같은 log를 확인할 수 있다.

```
...
2021-09-07 03:27:01.683 5337-5362/com.test.myapplication D/UserhabitLog: SCREEN_CHANGE => Background
2021-09-07 03:27:11.187 5337-5388/com.test.myapplication D/UserhabitLog: SCREEN_CHANGE => Quit
2021-09-07 03:27:11.421 5337-5364/com.test.myapplication D/UserhabitLog: NETWORK => Session data send (4)
```
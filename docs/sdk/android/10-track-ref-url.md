---
layout: default
title: 유입 경로 추적하기
parent: Android SDK
grand_parent: SDK
nav_order: 10
has_toc: false
---
# 유입 경로 추적하기

텐핑 서비스를 활용하고 계실 경우 유저해빗을 통한 어뷰징을 막을 수 있는 장점이 있습니다. 
단, 아래와 같이 추가적인 작업이 필요합니다. 

> **주의!**
안드로이드에서는 하나의 앱에서 하나의 리시버만 설정할 수 있습니다.

## **1. 유저해빗 인스톨 리시버를 한 개만 활용할 경우**

AndroidManifest.xml 파일에 다음과 같이 입력합니다.

```xml
<receiver
   android:name="io.userhabit.service.main.UserhabitInstallReceiver"
   android:exported="true">
 <intent-filter>
   <action android:name="com.android.vending.INSTALL_REFERRER" />
 </intent-filter>
</receiver>
```

## **2. 인스톨 리시버를 두 개 이상 활용할 경우**

하나의 리시버를 직접 구현하고 해당 리시버에서 다른 리시버들을 호출 합니다. 

아래와 같이 하나의 인스톨 리시버를 생성합니다.

```jsx
public class MultiInstallReceiver extends BroadcastReceiver {
   @Override
   public void onReceiver(Context context, Intent intent) {
    UserhabitInstallReceiver userhabitReceiver = new UserhabitInstallReceiver();
    userhabitReceiver.onReceive(context, intent);

    //다른 서비스의 리시버들을 동일한 방식으로 호출합니다.
   }
}
```

위와 같이 작성한 리시버를 AndroidManifext.xml 에 등록합니다.

```xml
<receiver
       android:name="com.yourpackage.MultiInstallReceiver"
       android:exported="true">
    <intent-filter>
        <action android:name="com.android.vending.INSTALL_REFERRER" />
    </intent-filter>
 </receiver>
```

## **3. 인스톨 리시버 확인 방법**

인스톨 리시버로부터 오는 데이터일 경우 실제 플레이스토어에서 설치 시에 데이터를 넘겨주기 때문에 테스트에 어려움이 있습니다. adb shell을 이용하여 인스톨 리시버를 호출하여 설정이 올바르게 되었는지 테스트합니다.

- 확인 방법
    1. 먼저 안드로이드 기기를 PC와 연결 하고, adb 실행 파일을 찾습니다.
    2. adb 파일은 안드로이드가 설치되어 있는 경로 안에 있습니다. 안드로이드 설치 경로를 기준으로 platform-tools 디렉토리 안에 adb 파일이 있습니다.

        ```bash
        Android/sdk/platform-tools
        ```

    3. adb shell을 실행합니다.

        ```bash
        #)adb shell
        ```

    4. 앱을 실행한 상태에서 알맞은 패키지명과 인스톨 리시버클래스 경로를 입력합니다.

        ```bash
        am broadcast -a com.android.vending.INSTALL_REFERRER
          -n <패키지명>/<인스톨 리시버 클래스 경로> --es "referrer" "Parameter"
        ```

        ex) 유저해빗 리시버를 이용할 경우

        ```bash
        am broadcast -a com.android.vending.INSTALL_REFERRER
          -n <패키지명>/io.userhabit.service.main.UserhabitInstallReceiver --es "referrer" "Parameter"
        ```

        ex) 여러개 리시버를 사용하기 위해서 별도의 인스톨 리시버를 만든 경우

        ```bash
        am broadcast -a com.android.vending.INSTALL_REFERRER
          -n <패키지명>/<직접 생성한 인스톨 리시버 클래스> --es "referrer" "Parameter"
        ```

    5. 올바르게 설정 되었다면 해당 명령어를 입력한 다음 안드로이드 로그 창에 태그명이`"UserhabitLog"`로 `"referrer : Parameter"`와 같이 입력한 값이 출력됩니다.
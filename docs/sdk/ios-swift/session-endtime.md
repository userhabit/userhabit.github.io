---
layout: default
title:  세션 종료시간 설정하기
parent: iOS-Swift
grand_parent: SDK
nav_order: 4
---

# 세션 종료시간 설정하기

유저해빗에서는 앱이 백그라운드로 이동한 후 일정 시간 동안 앱을 활성화하지 않을 경우 세션을 종료합니다. 
세션 종료 시간으로 지정된 기본값은 **10초**로 설정되어 있습니다. 해당 값은 아래와 같은 방법으로 수정이 가능합니다.

```swift
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
        UserHabit.sessionStart("YOUR-API-KEY")
        UserHabit.setSessionDelayTime(15.0) // 예) 10초(기본값)을 15초로 변경하는 경우
        self.window!.makeKeyAndVisible()
        return true
    }
```
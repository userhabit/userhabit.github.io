---
layout: default
title:  디버그 모드 활성화 하기
parent: iOS-Swift
grand_parent: SDK
nav_order: 7
---

# 디버그 모드 활성화 하기

디버그 모드를 활성화 하면 유저해빗 수집 과정에 대한 로그 및 수동 스크린샷 수집 모드를 활용하실 수 있습니다. 
수동 스크린샷 수집모드는 현재 베타 서비스 중이며, Production 모드에서는 활성화되지 않습니다. 

자세한 내용은  👉🏻 [스크린샷 취득하기](/docs/sdk/ios-swift/get-screenshot.html) 에서 "수동 스크린샷 수집 모드"에서 확인해주세요.

```swift
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        UserHabit.sessionStart(“YOUR-API-KEY”)
        UserHabit.setDebug(true)
    }
}
```
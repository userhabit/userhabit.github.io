---
layout: default
nav_order: 7
title:  디버그 모드 활성화 하기
parent: iOS-ObjectC
grand_parent: SDK
---

# 디버그 모드 활성화 하기

디버그 모드를 활성화 하면 유저해빗 수집 과정에 대한 로그 및 수동 스크린샷 수집 모드를 활용하실 수 있습니다. 
수동 스크린샷 수집모드는 현재 베타 서비스 중이며, Production 모드에서는 활성화되지 않습니다. 

자세한 내용은  👉🏻 [스크린샷 취득하기](/docs/sdk/ios-objectc/get-screenshot.html) 에서 "수동 스크린샷 수집 모드"에서 확인해주세요.

```objectivec
#import <UserHabit/UserHabit.h>

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [UserHabit SessionStart:@"YOUR-API-KEY" withAutoTracking:true];
    [UserHabit setDebug:YES];
    return YES;
}
```
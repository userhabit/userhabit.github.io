---
layout: default
nav_order: 9
title:  디바이스 구분자 랜덤 생성 기능
parent: iOS-ObjectC
grand_parent: SDK
---

# 디바이스 구분자 랜덤 생성 기능

유저해빗에서는 각각의 디바이스를 구분하기 위하여 iOS에서 제공하는`identifierForVendor(UUID)`값을 사용합니다. 해당 `identifierForVendor(UUID)`사용에 관하여 정책에 따라 해당 값을 수집하지 않기 위해서 아래와 같은 메소드를 통해서 임의로 지정된 값으로 대체 가능합니다.

```objectivec
#import <UserHabit/UserHabit.h>

@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [UserHabit enableDeviceRandomID]; // 추가
    [UserHabit SessionStart:@"YOUR-API-KEY"]; // 추가

    return YES;
}
```

⚠️ 해당 메소드는 반드시, `UserHabit.sessionStart("YOUR-API-KEY", withAutoTracking:false`메소드 이전에 실행하셔야 적용됩니다. 기존 디바이스 아이디를 수집한 상태에서 해당 메소드를 적용할 경우 이전 디바이스와 매칭이 되지 않는 점 유의하세요. (이로 인해, 유니크한 사용자 정보가 부정확해질 수 있습니다.)

⚠️ `UserHabit.sessionStart("YOUR-API-KEY");`메소드는 self.window를 alloc 하신 후에 삽입 하셔야 합니다.
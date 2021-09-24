---
layout: default
nav_order: 2
title:  추가 화면 구성하기
parent: iOS-ObjectC
grand_parent: SDK
---

# 추가 화면 구성하기

## **1. 사용자 정의를 통해 추가 화면 정의하기**

ViewController내에서 다양한 화면 구성을 통해 하나 이상의 화면을 표현하는 경우가 있습니다. 이 경우, 화면이 변경될 때마다 +setScreen:을 호출하시면 각각의 화면으로 분류하여 분석합니다.

```objectivec
- (void)viewWillAppear:(BOOL)animated {
    [super viewWillAppear:animated];
    [UserHabit setScreen:self withName:@"ScreenName"];

  }
```

## **2. 특정 화면 제외하기**

+setScreen:을 사용하여 화면을 분류해 분석하는 경우, ViewController가 사실상 화면으로써의 가치가 없어지는 경우가 발생합니다. 이 경우, 해당 ViewController가 자동으로 화면으로 정의되지 않도록 다음과 같이 추가합니다.

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [UserHabit SessionStart:@"YOUR-API-KEY" withAutoTracking:YES];

    NSArray *excluding = @[@"CustomNavigationController",
                           @"TabBarController",
                           @"UserhabitViewController"];

    [UserHabit excludeClasses:excluding];
    return YES;
}
```

## 3. 자동 수집 해제하기

모든 ViewController에서 자동으로 화면을 인식하고 싶지 않다면 아래 기능을 활용합니다. 이 때, 모든 화면을 +setScreen:으로 직접 정의해야 합니다.

```objectivec
#import <UserHabit/UserHabit.h>

@interface AppDelegate ()
@end
@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [UserHabit SessionStart:@"YOUR-API-KEY" withAutoTracking:true]; // 추가
    return YES;
}
```

## 4. UIAlert 화면 추적하기

UIAlert으로 정의한 화면에 대해서도 추적이 가능합니다. 아래와 같이 UIAlert 호출한 다음, 함수를 호출하여 사용합니다.

```objectivec
- (IBAction)testAlertButtonAction:(UIButton *)sender {

    UIAlertController* alert = [UIAlertController alertControllerWithTitle:@"My Alert"
                                   message:@"This is an alert."
                                   preferredStyle:UIAlertControllerStyleAlert];
    UIAlertAction* defaultAction = [UIAlertAction actionWithTitle:@"OK" style:UIAlertActionStyleDefault
   handler:^(UIAlertAction * action) {}];
    [alert addAction:defaultAction];
    [self presentViewController:alert animated:YES completion:nil];
    [UserHabit setScreen:self withName:@“UserHabit Alert"]; // 추가
}
```
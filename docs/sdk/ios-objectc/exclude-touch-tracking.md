---
layout: default
nav_order: 6
title:  사용자 터치 수집 제외하기
parent: iOS-ObjectC
grand_parent: SDK
---

# 사용자 터치 수집 제외하기

보안상의 이유로 특정 뷰 영역에 대한 터치를 수집하고 싶지 않다면 아래와 같이 등록하세요.

```objectivec
-(void)viewWillAppear:(BOOL)animated{
    [super viewWillAppear:animated];
    [UserHabit addSecretView:self.view];
}
```
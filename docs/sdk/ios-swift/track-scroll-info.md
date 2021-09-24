---
layout: default
title:  스크롤 데이터 추적하기
parent: iOS-Swift
grand_parent: SDK
nav_order: 3
---
# 스크롤 데이터 추적하기

iOS에서 제공하는 UIScrollView와 UITableView에 대해서 스크롤 분석이 가능합니다. 
아래 예시코드와 같이 해당하는 뷰를 등록하면 됩니다. (한 화면당 하나의 스크롤만 분석이 가능합니다.)

또한, 스크롤 분석에 필요한 스크린샷은 반드시 직접 수집해야 합니다.

## **1. 스크롤 스크린샷 취득하기**

스크롤 스크린샷을 취득하기 위해서는 👉🏻 [스크린샷 취득하기](/docs/sdk/ios-swift/get-screenshot.html) 에서 '수동 스크린샷 수집모드' 기능을 활용해야 합니다.

1. 먼저, 수동 스크린샷 수집모드를 활성화 합니다.
2. 스크롤 화면에서 스크롤 화면 수집 버튼을 누르면 자동으로 스크린샷을 수집합니다. (최대 1분의 시간이 소요되며, 스크린샷이 수집되는 동안 앱을 터치할 수 없습니다. 전원 버튼을 누르거나 앱을 종료하지 마세요. 동작이 완료되면 다시 앱이 활성화 됩니다.)

⚠️ 디바이스 해상도 width가 750px이 아닌 경우, 일부 데이터가 부정확하게 보일 수 있습니다.

## 2. 스크롤 추적을 위한 코드 적용

```swift
    
  override func viewWillAppear(_ animated: Bool) {
      UserHabit.addScrollView("scrollView", scrollView: mainTableView, rootViewController: self)
  }
```
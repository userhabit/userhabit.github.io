---
layout: default
title:  웹뷰 오브젝트 추적하기 (BETA)
parent: iOS-Swift
grand_parent: SDK
nav_order: 5
---

# 웹뷰 오브젝트 추적하기 (BETA)

아래와 같이 코드를 적용하시면, 웹뷰 내에서 오브젝트를 터치할 경우 해당 오브젝트의 정보가 수집됩니다.

```swift
override func viewDidAppear(_ animated: Bool) {
        webview.loadRequest(URLRequest(url:URL(string:urlString)!))
        UserHabit.addWebView(webview: webview)
 }
```

웹뷰의 오브젝트 이미지는 👉🏻 [스크린샷 취득하기](/docs/sdk/ios-swift/get-screenshot.html) 의 '수동 스크린샷 수집 기능'을 통해서만 수집할 수 있습니다.

## **1. 자바스크립트 유저해빗 API호출 가이드**

웹페이지 내에서 다양한 화면 구성을 통해 하나 이상의 화면을 표현하는 경우가 있습니다. 이 경우, 웹페이지가 변경될 때마다 아래 함수를 호출하시면 각각의 화면으로 분류하여 분석이 가능합니다. 

> **주의!**
자바스크립트로 유저해빗 API를 사용 하려면 반드시 해당 웹뷰를 +addWebview:를 통해 등록해주셔야합니다.

1. HTML

    ```html
    <button id='actionButton' onclick='yourOnClick()'> yourButton </button>
    ```

2. Javascript

    ```jsx
    function yourOnClick() {
        userhabitSetScreen('yourScreenName')
    }
    ```
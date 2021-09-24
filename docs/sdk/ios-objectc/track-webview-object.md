---
layout: default
nav_order: 5
title: 웹뷰 오브젝트 추적하기 (BETA)
parent: iOS-ObjectC
grand_parent: SDK

---

# 웹뷰 오브젝트 추적하기 (BETA)

아래와 같이 코드를 적용하시면, 웹뷰 내에서 오브젝트를 터치할 경우 해당 오브젝트의 정보가 수집됩니다.

```objectivec
- (void)viewDidAppear {
    NSURLRequest *request = [NSURLRequest requestWithURL:[NSURL URLWithString:urlString]];
    [webView loadRequest:request];
    [UserHabit addWebView:webView]; // 추가
 }
```

웹뷰의 오브젝트 이미지는 👉🏻 [스크린샷 취득하기](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%20%E1%84%8E%E1%85%B1%E1%84%83%E1%85%B3%E1%86%A8%E1%84%92%E1%85%A1%E1%84%80%E1%85%B5%20db2b4278ff5a4ddca3a14c42b2f4164d.md) 의 "수동 스크린샷 수집 기능"을 통해서만 수집할 수 있습니다.

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
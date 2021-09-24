---
layout: default
title: 웹뷰 오브젝트 추적하기 (BETA)
parent: Android SDK
grand_parent: SDK
nav_order: 5
has_toc: false
---
# 웹뷰 오브젝트 추적하기 (BETA)

아래와 같이 코드를 적용하시면, 웹뷰 내에서 오브젝트를 터치할 경우 해당 오브젝트의 정보가 수집됩니다.

```java
@Override
 protected void onCreate(@Nullable Bundle savedInstanceState) {     
  super.onCreate(savedInstanceState);     
  setContentView(R.layout.activity_webview);      

  mWebView.getSettings().setJavaScriptEnabled(true);  
  mWebView.loadUrl(“http://userhabit.io“);     
  WebViewClient webViewClient = new WebViewClient();     
  mWebView.setWebViewClient(webViewClient);      

  Userhabit.addWebView(mWebView, webViewClient); 
 }
```

웹뷰의 오브젝트 이미지는 👉🏻 [스크린샷 취득하기](/docs/sdk/android/get-screenshot.html) 의 "수동 스크린샷 수집 기능"을 통해서만 수집할 수 있습니다.

## **1. 웹뷰 스크롤 데이터 추적 API 호출 가이드**

아래와 같이 코드를 적용하시면 웹뷰 내의 콘텐츠 스크롤 분석이 가능합니다. 

> **주의!**
한 화면당 하나의 스크롤만 분석이 가능합니다.

```java
@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_webview);
      
    mWebView.getSettings().setJavaScriptEnabled(true); 
    
    mWebView.loadUrl(“http://userhabit.io“);
    WebViewClient webViewClient = new WebViewClient();
    mWebView.setWebViewClient(webViewClient);
    
    Userhabit.addWebView(mWebView, webViewClient); 
    Userhabit.addScrollView(mWebview) //addWebview 아래에 코드 적용
}
```

## **2. 웹뷰 스크롤뷰 수동 스크린샷 수집**

수동 스크린샷 수집 모드를 활용하여 웹뷰 스크롤뷰를 수집할 경우 아래의 코드를 적용해주세요.

> **주의!**
해당 버전 분기 코드는 API 19 이상이기 때문에 반드시 필요합니다.

```jsx
@Override
protected void onCreate(@Nullable Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
      
    if (Build.VERSION.SDK_INT > Build.VERSION_CODES.LOLLIPOP){ 
        WebView.enableSlowWholeDocumentDraw(); 
    } 
    
    setContentView(R.layout.activity_webview);

    mWebView.getSettings().setJavaScriptEnabled(true);
    mWebView.loadUrl(“http://userhabit.io“);
    WebViewClient webViewClient = new WebViewClient();
    mWebView.setWebViewClient(webViewClient);

    Userhabit.addWebView(mWebView, webViewClient);
    Userhabit.addScrollView(mWebview)

}
```

## **3. 자바스크립트 유저해빗 API호출 가이드**

웹페이지 내에서 다양한 화면 구성을 통해 하나 이상의 화면을 표현하는 경우가 있습니다. 이 경우, 페이지가 변경될 때마다 아래 함수를 호출하시면 각각의 화면으로 분류하여 분석이 가능합니다. 

> **주의!**
자바스크립트로 유저해빗 API를 사용 하려면 반드시 해당 웹뷰를 addWebview API를 통해 등록해주셔야합니다.

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
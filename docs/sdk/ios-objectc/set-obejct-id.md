---
layout: default
nav_order: 11
title: 오브젝트 아이디 설정
parent: iOS-ObjectC
grand_parent: SDK

---

# 오브젝트 아이디 설정

화면에 수집되는 오브젝트 아이디를 수동으로 지정하거나 자동으로 생성합니다. 아이디 생성의 우선 순위는 다음과 같습니다.


## 아이디 생성의 우선순위

우선순위|설명|결과물
--|--|--
1. accessibilityIdentifier를 설정한 경우	| 애플에서 제공하는 오브젝트의 유니크한 키값을 지정할 수 있습니다. 해당 값이 그대로 오브젝트 아이디로 사용됩니다.<br>👉🏻[애플 가이드 문서](https://developer.apple.com/documentation/uikit/uiaccessibilityidentification/1623132-accessibilityidentifier?language=objc)	| TestObjectId
2. 오브젝트에 이벤트가 설정된 경우	| 1번에 해당 하지 않는 경우 오브젝트의 Target을 이용해 아이디가 생성됩니다.<br>`[UIViewController::target(layerIndex)]` | FirstViewController::backButtonAction(4)
3. 오브젝트에 이벤트가 설정되지 않은 경우|1번과 2번에 모두 해당하지 않는 경우 오브젝트의 클래스 명을 이용해 아이디가 생성됩니다. <br> `[UIViewController::NSObject(layerIndex)]`|	FirstViewController::UIButton(4)
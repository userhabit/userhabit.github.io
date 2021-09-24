---
layout: default
title: 추가 화면 구성하기
parent: Android SDK
grand_parent: SDK
nav_order: 2
has_toc: false
---
# 추가 화면 구성하기

UserHabit 서비스는 기본적으로 한 개의 Activity를 하나의 화면으로 자동 정의 합니다.
필요한 경우, 아래의 기능을 활용해 한 개의 Activity를 여러 화면으로 쪼개어 정의할 수 있습니다.

## **1. ViewPager로 구성된 화면 분석하기**

하나의 Activity를 ViewPager 객체를 이용하여 여러 화면을 구성할 경우 이를 위한 별도의 함수를 제공하고 있습니다.
(ViewPager에 등록되는 화면이 한번 더 여러 화면으로 분할되어 사용될 경우 아래 2.사용자 정의 기능을 활용하세요)

```java
@Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);

      mViewPager = (ViewPager) findViewById(R.id.vpPager);
      mAdpater = new MyPagerAdapter(getSupportFragmentManager());
      mViewPager.setAdapter(mAdpater);
      Userhabit.setViewPager(mViewPager); 
  }

```

## **2. 사용자 정의를 통하여 추가 화면 정의하기**

Activity 내에서 화면을 다양하게 구성해 한 개 이상의 화면을 표현하는 경우가 있습니다. 이 경우에, 화면이 변경 될 때 마다 아래 함수를 호출하시면 각각의 화면으로 분류하여 분석합니다. 

> **주의!**
해당 함수는 onResume() 함수 이후에 적용하셔야 올바르게 동작합니다.

```java
@Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);

        Button btn = findViewById(R.id.button);
        btn.setOnClickListener(new View.OnClickListener() {
          @Override
          public void onClick(View v) {
              Userhabit.setScreen(this, "테스트 화면");
          }
         });
  }

```

## **3. 특정 Activity 화면 제외하기**

setScreen 함수를 사용하여 화면을 분류하는 경우, Activity가 사실상 화면으로의 가치가 없어지는 경우가 발생합니다. 이 같은 경우, 해당 Activity가 자동으로 화면 정의가 되지 않도록 다음과 같이 추가합니다.

```jsx
public class YourApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        ArrayList<Class<? extends Activity>> list = new ArrayList<>();
        list.add(MainActivity.class);
        Userhabit.setExcludingClasses(list);
        Userhabit.start(this);
        
    }
}
```

## **4. Activity 자동 수집 해제하기**

모든 Activity에서 자동으로 화면 인식을 하고 싶지 않다면 아래 기능을 활용합니다. 

> **주의!**
이때에는 모든 화면을 setScreen으로 직접 적용하셔야 합니다.

```jsx
public class YourApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        Userhabit.setManualActivityMode(true);
        Userhabit.start(this);
    }
}
```

## **5. 다이얼로그 화면 추적하기**

Dialog객체로 정의한 화면에 대해서도 추적이 가능합니다. 아래와 같이 Dialog의 show(); 호출 후에 아래와 같이 함수를 호출하여 사용합니다.

```jsx
private void showDialog() {
    mDialog.show();
    Userhabit.setScreen(mDialog, "다이얼로그_화면"); 
  }
```
---
layout: post
title:  뷰(View), 뷰 그룹(ViewGroup), 레이아웃(Layout)
categories: Android
comments: true
---

### View와 ViewGroup, Layout의 개념<br>

'View'란?<br>

UI의 구성 요소 중 가장 추상화된 개념으로서, 화면에 표시되는 가장 기본적인 요소를 말한다.<br>
ex) 그림, 텍스트, 버튼 등 화면에 표시되는 모든 요소가 View로 간주된다.<br>

'ViewGroup이란?'<br>

ViewGroup은 View를 상속받으면서 특별히 여러 개의 구성 요소들을 포함하는 View이다. ViewGroup은 여러 개의 View들을 자식 뷰(Child View)로 가지면서 View의 위치를 조정하고 그룹화하여 관리할 수 있다. ViewGroup에 포함되어 있는 'View'를 가르켜 '자식 뷰(Child View)'라고 하고, ViewGroup을 '부모 뷰(Parent View)'라고 한다.<br>

ViewGroup은 View를 Group형태로 포함시킬 수 있는 클래스의 추상화된 개념으로, 실제로 사용되는 것이 ViewGroup를 상속받은 'Layout'이다.<br>
'Layout'은 포함된 View를 배치할 수 있는 클래스이다.<br>

### 전체적인 학습내용을 복습한다.<br>
1. View는 안드로이드의 UI 요소 중 가장 기본이 되는 요소이다.<br>
2. ViewGroup은 다른 여러 View를 포함시킬 수 있는 특별한 View이다. ViewGroup을 사용하면 View를 그룹화하여 관리할 수 있다.<br>
3. 레이아웃은 ViewGroup의 실제 구현 클래스이며 자식 뷰를 어떻게 배치할지 결정한다. 자주 사용하는 레이아웃에는 LinearLayout, RelativeLayout, ConstraintLayout등이 있다.<br>
   

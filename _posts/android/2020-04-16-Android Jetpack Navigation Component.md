---
layout: post
title:  Android Jetpack Navigation Component
categories: Android
comments: true
---

### Android Jetpack Navigation Component<br>

이번 포스팅에서는 Jetpack Navigation Component를 활용하여 Fragment간의 전이 처리하는 것에 대해서 배워 볼 것이다.<br>

<strong><font color="Blue">① app gradle에 dependencies 추가하기</font></strong> <br>

    def nav_version = "2.3.0-alpha05"
    // Kotlin
    implementation "androidx.navigation:navigation-fragment-ktx:$nav_version"
    implementation "androidx.navigation:navigation-ui-ktx:$nav_version"

    def material_version = "1.2.0-alpha05"
    implementation "com.google.android.material:material:$material_version"

※ navigation graph 기능

(1) resouce - [New Resource File] - (File name : nav_graph / Resource type : Navigation)<br>
(2) 위의 nav_graph 파일에 화면에 보여질 UI의 화면 설계구조를 구조화시킬 수 있다.<br>
(3) activity_main.xml 에서 <fragment> tag로 화면을 채우는데 <strong>이 부분이 각각 생성한 Fragment layout을 inflate하는 부분</strong>이 될 것이다.<br>
이 fragment tag안에 속성에서 살펴볼 것은, <strong>defaultNavHost = "true"와 app:navGraph = "@navigation/nav_graph" 인데 두번째 navGraph 속성은 navigation type의 layout에 생성할 layout의 구조를 setting하겠다는 의미, 마지막으로 android:name="androidx.navigation.fragment.NavHostFragment"속성도 필수적으로 설정해주어야 한다.</strong><br>

(4) 작성한 Fragment layout파일(*.xml)에서 가장 상단 tag의 속성에 <strong>tools:context = "xxxxxFragment" </strong>라고 지정해주어야 한다.<br>
이 layout 파일이 어느 fragment 클래스 파일과 관련이 있는지 표시하기 위해서이다.<br>

<strong><font color="Blue">② MainActivity에서는 화면의 fragment 태그에서 fragment 레이아웃을 보여주는 기능만 하므로, 실질적인 Navigation 객체를 만들어서 처리해주는 것은 Fragment class에서 해줄 것이다.</font></strong><br>

(1) onViewCreated() 메소드에서 property로 선언한 NavController 타입의 변수를 초기화시켜준다. <br>

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        // reference of the view
        navController = Navigation.findNavController(view)
        view_transactions_btn.setOnClickListener(this)
        send_money_btn.setOnClickListener(this)
        view_balance_btn.setOnClickListener(this)
    }

이 MainFragment도 nav_graph에 등록된 Fragment이기 때문에 navController객체의 생성이 가능하다. <br>   

(2) 이제 이 navController를 이용해서 각 버튼의 onClickListener의 이벤트를 구현할 것이다.<br>

    override fun onClick(v: View?) {
      // backStack관리가 자동으로 이루어지기 때문에 편리하다.
      when(v!!.id){
          R.id.view_transactions_btn -> navController.navigate(R.id.action_mainFragment_to_viewTransactionFragment)
          R.id.send_money_btn -> navController.navigate(R.id.action_mainFragment_to_chooseRecipientFragment)
          R.id.view_balance_btn -> navController.navigate(R.id.action_mainFragment_to_viewBalanceFragment)
      }
    }

위의 ②-(1)과 (2)의 과정을 다른 Fragment에서도 작성을 작성해준다. <br>

<strong><font color="Blue">③ 다음 과정에서는 animation, bundle을 추가하는 과정이다.</font></strong><br>







### 전체적인 학습내용을 복습한다.<br>
1. <br>
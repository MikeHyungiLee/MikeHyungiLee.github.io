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

ex)

    ....
    <fragment
        android:id="@+id/mainFragment"
        android:name="com.hyungilee.androidjetpacknavigationsample.MainFragment"
        android:label="fragment_main"
        tools:layout="@layout/fragment_main" >
          <action
            android:id="@+id/action_mainFragment_to_chooseRecipientFragment"
            app:destination="@id/chooseRecipientFragment"
            app:popEnterAnim="@anim/slide_in_left"
            app:popExitAnim="@anim/slide_out_right"
            app:enterAnim="@anim/slide_in_right"
            app:exitAnim="@anim/slide_out_left"
            app:popUpTo="@id/mainFragment"
            app:popUpToInclusive="true"/>
     ....

backStack이나 Back버튼을 눌렀을때 적용되는 animation효과는 popExitAnim 속성이다. <br>

다음 어플을 제작할때 생각해봐야 하는 부분은 대부분의 어플에 있는 Login 기능이다. <br>

로그인이 성공한 뒤에 Back 버튼을 누르게 되면, 이전의 로그인 화면으로 돌아가는 것이 아닌 어플자체가 화면에서 사라지고 단말기의 Background가 표시됨을 알 수 있다. (로그인 완료된 후에 Back버튼을 누른다고 다시 로그인 화면으로 돌아가는 것은 non sense상황)<br>

이 이벤트 처리 동작에 대해서 생각해보자.<br>
Back버튼을 누른다고 이전화면으로 돌아가지 않고, BackStack에서 실행되는 Task들을 모두 종료시키는 것을 해보자.<br>

<strong>popUpTo and popUpToInclusive</strong><br>
① popUpTo : Back 버튼을 눌렀을때 이벤트　<br>
② popUpToInclusive : true(clear everything to navigate) or false(leave it) <br>

<strong>※ Android 공식 : </strong>[Get started with the Navigation component](https://developer.android.com/guide/navigation/navigation-getting-started)

<strong><font color="Blue">Fragment 간에 값을 보내기</font></strong><br>

(1) 먼저 아래 sample 코드를 보고 nav_graph.xml에서의 설정에 대해서 이해해보도록 하자. <br>
우선 화면은 <strong><font color="Red">specifyAmountFragment.xml -> confirmationFragment.xml</font></strong>전이를 하게 되는데, 화면전이가 일어날때 값을 bundle의 형태로 넘겨준다. <br>

보내고자하는 데이터를 입력하는 Fragment 태그에서 name이 recipient, defaultValue가 None으로 된 태그를 추가해주고, <br>
받는 Fragment 태그에서도 똑같이 argument태그를 추가해주고, 추가적으로 name이 "amount", argument 타입이 보내고자하는 데이터의 data class의 경로를 지정해준다.<br>

    ....
    <fragment
        android:id="@+id/confirmationFragment"
        android:name="com.hyungilee.androidjetpacknavigationsample.ConfirmationFragment"
        android:label="fragment_confirmation"
        tools:layout="@layout/fragment_confirmation">

        <argument android:name="recipient"
                  android:defaultValue="None"/>

        <argument android:name="amount"
                  app:argType="com.hyungilee.androidjetpacknavigationsample.Money"/>

    </fragment>

    <fragment
        android:id="@+id/specifyAmountFragment"
        android:name="com.hyungilee.androidjetpacknavigationsample.SpecifyAmountFragment"
        android:label="fragment_specify_amount"
        tools:layout="@layout/fragment_specify_amount" >

        <argument android:name="recipient"
                  android:defaultValue="None"/>
    ....              

(2) 다음으로 수취인 이름을 등록하는 Fragment(chooseRecipientFragment.kt)파일에서 아래와 같이 bundle의 형태로 수취인 데이터를 넘겨준다.<br>

    R.id.next_btn -> {
          if(!TextUtils.isEmpty(input_recipient.text.toString())){
              val bundle = bundleOf("recipient" to input_recipient.text.toString())

              navController.navigate(
                  R.id.action_chooseRecipientFragment_to_specifyAmountFragment,
                  bundle
              )
          }
    }

(3) 데이터를 받는 Fragment(SpecifyAmountFragment.kt)파일에서는 아래와 같이 bundle 형태로 데이터를 취득하는 부분을 작성한다.<br>

    lateinit var recipient: String

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        recipient = arguments?.getString("recipient")!!
    }

Parcelable 데이터를 받는 경우에는 getParcelable("[키값]") 로 해서 취득하며, Parcelable로 취득할 객체의 class는 아래와 같이 작성해준다. 여기서 값의 초기화는 "onCreater()"메소드에서 처리하며, 화면에 보여질 view의 초기화는 메소드명대로 "onViewCreated()"메소드에서 처리해준다.<br>

    @Parcelize
    data class Money(val amount: BigDecimal): Parcelable



### 전체적인 학습내용을 복습한다.<br>
1. <br>

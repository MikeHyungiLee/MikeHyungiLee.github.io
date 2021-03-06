---
layout: post
title:  Java MVVM Part1 ~ 3
categories: Android-Architecture
comments: true
---

### #1 Android MVVM Architecture Tutorial - Introduction<br>
### #2 Android MVVM Architecture Tutorial - Project Setup<br>
### #3 Android MVVM Architecture Tutorial - Using Data Binding<br>

<strong>참고</strong>:[https://www.youtube.com/watch?v=67bdklHmXA8&list=PLk7v1Z2rk4hjVaZ8DZKe8iT9RIM9OUrwp&index=1](https://www.youtube.com/watch?v=67bdklHmXA8&list=PLk7v1Z2rk4hjVaZ8DZKe8iT9RIM9OUrwp&index=1)<br>

MVVM(Model View View Model)<br>

Why Design Pattern?<br>

(1) Makes the code more understandable.<br>
(2) Makes the code maintainable for long run.<br>
(3) Makes the project loosely coupled.<br>
(4) Makes the code testable.<br>
(5) Making changes, adding new features are easy.<br>
<strong>Design Patter에 따라서 앱을 만들면, 나중에 다른 개발자들이 앱을 파악하는데 매우 도움이 되고, 더 나아가 코드를 운용보수하는데도 도움이 된다. </strong><br>
<strong>또한 코드를 테스트하고, 새로운 기능을 추가를 쉽게 할 수 있다.</strong><br>

<strong><font color="Red">Architectural Principles</font></strong><br>

(1) Separation of Concerns<br>

(2) Drive UI from Model <br>

Why MVVM?<br>
(1) MVC <br>
(2) MVP <br>
(3) MVVM (Google recommend) <br>

기존에 살펴보았던 MVVM Design Pattern의 구조를 다시 되짚어보면,<br>
(1) UI를 담당하는 Activity/Fragment<br>
(2) Life cycle을 담당하는 ViewModel [LiveData] <br>
(3) ViewModel에서 데이터를 취득하는 경로 "Repository"<br>
(4) "Repository"에 데이터를 제공하는 <strong>"Room - SQLite" Local database(=Model)</strong>, 원격 서버에서 데이터를 제공하는 <strong>"Remote Data Source" - "Retrofit - WebService"</strong><br>

위의 구조로 구성되어있는 것을 배웠다. 앱은 기본적으로 <strong>Model(Local storage)</strong>를 통해 우선적으로 데이터를 취득한다.<br>
따라서, 인터넷 연결에 문제가 생겨도 앱의 사용에 있어서는 문제가 없게 된다.<br>

이제 Kotlin으로 Room Database를 포함한 프로젝트를 생성해보자.<br>

<strong>App level의 gradle에 아래의 dependencies를 추가해준다.</strong><br>
상단에는 아래의 apply plugin: 을 선언해주고,  

    //kotlin kapt and navigation safeargs plugin
    apply plugin: 'kotlin-kapt'
    apply plugin: "androidx.navigation.safeargs"

android{} 안에 buildTypes의 아래에 추가해준다. (dataBinding compiler 추가)

    dataBinding{
        enabled = true
    }

(1) Retrofit and GSON<br>
(2) Kotlin Coroutines<br>
(3) ViewModel and LiveData<br>
(4) New Material design<br>
(5) Kodein Dependency Injection<br>
(6) Android Room<br>
(7) Android Navigation Architecture<br>

<strong>Project level의 gradle에 아래의 class Path를 추가해준다.</strong><br>

    //Android Navigation Safe Args Classpath
    classpath "androidx.navigation:navigation-safe-args-gradle-plugin:2.2.0-alpha02"

<strong>"gradle.properties"에 아래의 내용을 추가해준다.</strong><br>

    android.databinding.enableV2=true

<strong><font color="Red">※ Project package 구성</font></strong><br>

<table>
  <tr>
    <td><strong><font color="Blue">Package(level-1)</font></strong></td>
    <td><strong><font color="Blue">Package(level-2)</font></strong></td>
    <td><strong><font color="Blue">Package(level-3)</font></strong></td>
  </tr>
  <tr>
    <td>① data<br></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>② ui <br></td>
    <td>auth</td>
    <td>(I) AuthListener.kt <br>
        (C) AuthViewModel.kt<br>
        (C) LoginActivity.kt<br>
        (C) SignupActivity.kt<br>
    </td>
  </tr>
  <tr>
    <td></td>
    <td>home</td>
    <td></td>
  </tr>
  <tr>
    <td>③ util <br></td>
    <td>
       → ViewUtils.kt <br>
      (1) Context. 확장함수 형태로 toast 메시지를 띄우는 메소드를 작성<br>
    </td>
    <td></td>
  </tr>
</table>

위의 도표와 같은 구조로 패키지를 구성하였다. <br>

<img src="/images/android/2020-04-19/2020-04-19 data binding note(1).png" alt="blog capture" width="500" title="capture img"><br>

다음으로 할 작업은 로그인 페이지 처리부분을 구현할 것이다.<br>
Login할때 UI(Activity/Fragment)상에서 ID와 Password를 입력하고, 입력한 데이터가 ViewModel, Repository, Remote Data Source 순으로 이동해가면서 Validation 체크를 하게 된다.<br>

이때 Login할때 입력했던 데이터(ID, Password)는 editText에 입력한 값을 getter 메소드로 취득해서 처리하지 않고, <strong><font color="Red">"Data binding처리"</font></strong>를 해서 처리를 해줄 것이다. <br>

노트필기 캡쳐의 하단부에 작성한 Data binding하는 방법에 대한 내용을 다시 한 번 정리해본다.<br>
<strong><font color="Blue">※ Data binding하는 방법</font></strong><br>
(1) 기존의 layout 파일에서 Top-level tag를 감싸는 <layout></layout> 태그를 만들어준다.<br>
    (만들어준 layout태그에 <strong>xmlns:~</strong>로 시작하는 tag를 <layout> 안에 붙여넣는다)<br>
(2) 이제 실제 binding해줄 <data> 태그를 <layout>과 <androidx.~>(실제 UI 구성 코드) 사이에 작성해준다. data tag는 아래와 같은 형태로 작성해준다. <br>

    <data>
        <variable name="viewmodel"
                  type="(viewModel class의 full경로)"/>
    </data>

(3) UI 구성코드에 있는 editText(email, Password)의 text 속성에 <strong>"@={viewmodel.email}"</strong> 와 같은 형태로 작성해준다. <strong>onclick 속성의 경우에는 "@{viewmodel:onLoginButtonClick}"과 같은 형태로 작성해준다.</strong> <br>

<img src="/images/android/2020-04-19/2020-04-19 data binding note(2).png" alt="blog capture" width="500" title="capture img"><br>

이제는 AuthViewModel 클래스와 LoginActivity의 관계 성립을 위해 <strong><font color="Red">AuthListener 인터페이스</font>를 작성한다.</strong><br>
AuthListener 인터페이스에는 "성공, 실패, 시작"했을때 Toast 메시지를 처리할 메소드를 작성해준다.<br>

LoginActivity에는 AuthListener를 구현해서 override 메소드를 구현한다.<br>
<strong><font color="Red">이제 Activity 클래스와 AuthViewModel 클래스를 binding해줄 것이다.</font></strong><br>
onCreate()메소드에서 <br>

    // binding의 타입은 레이아웃의 이름을 기준으로 layout name conversion이 일어난다.
    val binding: ActivityLoginBinding = DataBindingUtil.setContentView(this, R.layout.activity_Login)

    val viewModel = ViewModelProviders.of(this).get(AuthViewModel::class.java)
    // layout파일에서 사용할 viewmodel 에 실제 viewmodel 클래스 객체를 주입시켜준다.
    binding.viewmodel = viewModel
    // LoginActivity에서 구현을 해줬기 때문에 "this" 해주면 된다.
    viewModel.authListener = this

***

<strong>이제 실제 remote server로 입력한 email과 password를 비교하여 로그인 처리를 할 수 있도록 AuthViewModel과 Repository의 상호작용 처리하는 부분을 배워 볼 것이다.</strong><br>

### 전체적인 학습내용을 복습한다.<br>
1.

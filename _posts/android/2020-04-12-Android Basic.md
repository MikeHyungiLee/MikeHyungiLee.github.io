---
layout: post
title:  Activity, 명시적 Intent(Explicit Intent), 암시적 Intent(Implicit Intent) 
categories: Android
comments: true
---

이번 포스팅에서는 안드로이드의 기초적인 부분을 정리할 것이다. 이는 나중에 안드로이드를 모르는 사람에게 기초적인 부분을 좀 더 잘 설명할 수 있기 위함이다.<br>

<strong><font color="Blue">Activity?</font></strong>
사용자와 상호 작용이 가능한 UI, 즉 '활성화된 상태의 화면'을 말한다.<br>

Activity는 단일 화면이기 때문에, 각각의 독립된 단일 화면으로 나타낸 화면설계도(스토리 보드)의 화면은 각각의 Activity로 구성한다.<br>
비슷한 구성이거나 약간 다른 Activity같은 경우는 Activity를 통합하고 조건에 따라서 화면의 요소만 바꿔주면 된다.<br>
사전에 스토리 보드를 사용하여, 화면 설계를 하게 되면, 서로 비슷한 작업들을 사전에 파악하여 작업량을 줄이는 것이 가능하다. (화면설계의 중요성)<br>

여러 개의 화면을 Activity로 구성했을 때 화면 전환을 위해 사용하는 것이 바로 'Intent'이다.<br>

<strong><font color="Blue">Intent?</font></strong><br>
Intent는 안드로이드에서 앱 구성 요소 간의 작업을 요청할 수 있는 메시지 객체이다. <br>

<br>Intent의 기본적인 용례<br>
<table>
  <tr>
    <td width="300">사례</td>
    <td width="700">설명</td>
  </tr>
  <tr>
    <td>액티비티 시작</td>
    <td>Activity는 사용자와 상호 작용이 가능한 단일 화면이다. Activity의 새 인스턴스를 시작하기 위해 startActivity()메소드를 사용하여 Intent를 전달할 수 있습니다. 호출한 Activity가 완료되었을 때 결과를 수신하기 위해서는 startActivityForResult를 사용한다.</td>
  </tr>
  <tr>
    <td>서비스 시작</td>
    <td>Service는 UI없이 Background에서 작업을 수행하는 요소이다. Service를 시작하기 위해서는 startService()메소드를 사용하여 Intent를 전달한다. </td>
  </tr>
  <tr>
    <td>브로드캐스트(broadcast)전달</td>
    <td>브로드캐스트는 모든 앱이 수신할 수 있는 메세지로, sendBroadCast(), sendBroadCastOrder(), sendStickyBroadcast 메소드에 Intent를 전달하여 BroadCast를 전달할 수 있다.</td>
  </tr>
</table>
<br>
<table>
  <tr>
    <td width="200">Click 이벤트 리스너 등록방법</td>
    <td width="400">장점</td>
    <td width="400">단점</td>
  </tr>
  <tr>
    <td>XML onClick</td>
    <td>레이아웃 XML 파일에서 View 객체들의 ID를 신경쓰지 않아도 된다. 심지어 ID가 없어도 된다.</td>
    <td>메소드가 없거나, 이름이 틀리거나, 파라미터 형태가 다르면 에러가 발생하고, 앱이 동료된다. 이러한 에러는 보통 Runtime(실행)중에 발견된다.</td>
  </tr>
  <tr>
    <td>View.setOnClickListener</td>
    <td>에러 발생을 컴파일 시에 미리 알 수 있다. Kotlin의 경우 Android Extension 기능으로 findViewById()가 필요 없어 소스가 간결하다.</td>
    <td>View 객체의 ID에 민감하다. 반드시 해당 View의 ID가 존재해야 하며, 레이아웃 구성이 복잡한 경우라면 View 객체들의 ID를 전부 이름 짓기 곤란한 경우가 있다.</td>
  </tr>
</table>
<br>
하지만, 코틀린 코드에서는 setOnClickListener를 사용하는 방법을 활용하는 것이 좋다. 실행과정에서 에러를 발견하는 것보다는 사전에 에러를 발견하는 것이 메리트가 크다고 판단된다.<br>

### 인텐트 유형 및 구성요소 <br>
Intent는 '기본 구성 요소 간의 통신을 위한 메세지 객체'이다. Activity를 시작하기 위해서 Intent를 사용하는 방법은 크게 2가지 유형이 있다. 그 2가지 유형을 '명시적 호출'과 '암시적 호출'이라고 부른다.<br>
<strong><font color="Red">명시적 호출(Intent) : </font></strong>시작할 기본 구성 요소(Activity, Service)등의 '이름'을 정확하게 알고 있을 때 사용한다. 여기서 '이름'이란 패키지명까지 포함한 완벽한 이름을 말한다. 명시적 인텐트는 보통 앱 자신의 구성요소를 호출할 때 사용한다. <br>

ex) Intent(Package Context, 타겟이 되는 구성요소의 Class)<br>
<strong>Context란?</strong><br>
애플리케이션이 가지고 있는 '환경 정보'에 대한 인터페이스로서, 이때의 '환경정보'란 애플리케이션의 패키지 이름, 리소스 정보 등 애플리케이션이 실행되고 있는 환경의 요소들을 일컫는다. <br>
Activity는 Context를 상속받기 때문에, 특정 Context 대신에 '자기자신'을 전달한다. 그러므로, 현재 실행되는 Activity의 애플리케이션 환경정보가 전달된다.<br>
<table>
  <tr>
    <td width="300">구성요소</td>
    <td width="700">설명</td>
  </tr>
  <tr>
    <td>Component name</td>
    <td>Component name은 실행하고자 하는 기본 구성요소의 명확한 이름이며, Intent가 명시인지, 암시인지 구분하는 요소가 된다.</td>
  </tr>
  <tr>
    <td>Action</td>
    <td>
      Action은 수행할 작업을 의미한다. <br>
      'ACTION_VIEW'와 같은 작업은 Activity가 사용자에게 특정 화면을 보여주도록 요청한다. 따라서 ACTION_VIEW 액션은 갤러리 앱의 특정 사진을 보여줄 경우 등에도 사용된다.
    </td>
  </tr>
  <tr>
    <td>Data</td>
    <td>Data는 Action에 따라 필요한 Data를 함께 보낼 때 사용한다. 예를 들어 갤러리에서 특정 사진을 편집해야 하는 경우 Data에 사진 정보에 대한 데이터를 같이 보낼 수 있다.</td>
  </tr>
  <tr>
    <td>Category</td>
    <td>Category는 인텐트를 처리하는 구성 요소에 대한 '분류'를 의미한다. 예를 들어 'CATEGORY_LAUNCHER'는 이 Activity가 런처에서 보여지고 앱이 시작될 때 사용되는 화면임을 의미하는 정보이다.</td>
  </tr>
  <tr>
    <td>Extras</td>
    <td>작업을 수행하기 위해 필요한 추가 정보이다. 보통은 Key, Value 타입의 정보를 전달하며, Bundle 객체로 전달할 수 있다.</td>
  </tr>
  <tr>
    <td>Flags</td>
    <td>Intent에 대한 Meta정보이다. 특정 구성 요소를 실행할 때 추가 정보로 활용될 수 있다. 예를 들어 Activity를 실행할 때 현재가지 실행된 모든  Activity를 실행할 때 현재까지 실행된 모든 Activity 스택을 초기화하고 실행하는 등의 작업을 할 수 있다.</td>
  </tr>
</table>
<br>
<strong><font color="Red">암시적 호출 : </font></strong>시작하는 구성요소(Activity, Service)의 이름을 명확하게 적지는 않지만, 일반적인 작업 유형을 선언하여 그 작업을 수행할 수 있는 구성 요소를 호출한다.<br>
<strong><font color="Blue">예를 들어</font></strong> <strong>작성하고 있는 앱에서 위치를 지도에서 표시하고 싶은 경우,</strong>이 경우 직접 구현하는 것도 방법이지만, 이미 사용자의 핸드폰에 설치된 '지도 애플리케이션'을 사용할 수도 있다. 사용자의 핸드폰에 이미 설치된 지도 애플리케이션이 <strong>'구글 지도'</strong> 일수도, <strong>'네이버 지도'</strong>일수도 있으며, 또는 그 구성요소의 명확한 이름을 알 수 없는 경우도 있다. <strong><font color="Red">바로 이러한 경우에 '암시적 인텐트'를 사용한다.</font></strong><br>

### 전체적인 학습내용을 복습한다.<br>
1. Intent는 구성 요소 간의 작업을 요청할 수 있는 메시지 객체이다.<br>
2. Intent의 유형에는 명시적, 암시적 유형이 있다.<br>
3. 같은 애플리케이션 내에서 화면 전환을 위해서는 명시적 Intent를 생성하고, startActivity()함수를 사용한다.<br>
4. <strong><font color="Red">암시적 Intent는 Component Name은 없고, 대신 작업 유형을 나타내는 Action을 지정한다.</font></strong><br>

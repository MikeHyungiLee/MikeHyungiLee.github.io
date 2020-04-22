---
layout: post
title:  (9) How to build beautiful UIs with Flutter Widgets
comments: true
categories: Flutter
---

### Flutter의 Widgets을 활용해서 UI를 작성해보자.<br>

MiCard (간단히 나의 소개를 하는 앱 프로젝트)를 만들어보면서 Flutter 앱 개발에 필요한 요소들을 공부해 나갈 것이다.<br>

이건 팁인데 GitHub 검색창에 Flutter를 검색해서 다른 사람의 소스코드들을 볼 수 있으니, 시간이 될때 다른 사람의 소스코드를 많이 보도록 하자.<br>

<strong>본격적으로 프로젝트를 시작하기 전에 <font color="Red">Hot Reload and Hot Restart</font>에 대해서 배워 볼 것이다.</strong><br>

<strong><font color="Blue">Flutter의 Hot reload기능을 사용하기 위해서는 Stateless Stateful Widgets에 대한 이해가 필요하다.</font></strong>

아래는 StatelessWidget의 사용의 예이다. <strong><font color="Red">stless를 작성하면 Stateless class가 자동완성된다.</font></strong><br>
<img src="/images/flutter/2020-04-21/2020-04-21 flutter stateless widget.png" alt="blog capture" title="capture img"><br>

이 기능을 이용하면 Flutter는 즉시 코드상의 변화를 Emulator에 반영한다.<br>

<strong>이 Hot Reload 기능을 사용하기 위해서는 우리는 <font color="Red">"StatelessWidget"</font>을 상속받는 클래스를 작성해서 이를 main() function에 넣어주어야 한다.</strong><br>
Stateless Widget 클래스를 상속하면 build method를 내부에 구현하게 되는데, 이 메소드는 앱의 코드 속성이 바뀔때마다 자동으로 화면을 갱신시켜준다.<br>

<img src="/images/flutter/2020-04-21/2020-04-21 hot reload.png" alt="blog capture" title="capture img" width="400"><br>

마치 화면에 바로 붓으로 페인팅을 해주는 듯이 앱을 만들어준다.<br>

<strong>우리는 개발을 할때 코드를 치고(Write code) <---> 코드를 테스트하는(Test code) 반복하는 작업을 한다. Flutter는 이 cycle의 시간을 단축시켜준다. </strong><br>

우리가 native Android/iOS 앱을 개발을 할때 Cold한 상태로 앱을 실행한다. Emulator를 실행하는데 시간이 오래걸린다. <br>

<strong>Flutter에서의 또 다른 장점 중에 하나는 <font color="Blue">현재 화면중에 표시되어있는 데이터가 있다면, 이 데이터의 상태는 유지한 상태에서 디자인의 변경만 화면에 적용</font>시킬 수 있다.</strong><br>

만약에 화면에 있는 데이터를 초기화 시킴과 동시에 화면의 디자인을 변경하고 싶다면, <strong><font color="Red">"Hot reload(번개표시)"옆에 있는 Hot restart(초록색 원형 화살표 표시)를 클릭하면 된다. Hot restart로 emulator를 다시 시작하는 것보다 훨씬 빠른 속도로 화면에 반영되는 것을 확인할 수 있다.</font></strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter hot restart.png" alt="blog capture" title="capture img" width="400"><br>

하나의 재미있는 컨셉으로 이 개념을 이해해보자.

<img src="/images/flutter/2020-04-21/2020-04-21 flutter example.png" alt="blog capture" title="capture img" width="400"><br>

위에 케리어 백이 하나 있다. 여행을 갈때 매일과 같이 싸야되는 물건과 목적지에 따라서 추가적으로 챙겨야 되는 물건이 있다고 가정하자. 이런 경우에는 공통적으로 싸야되는 물건은 고정적으로 준비를 해두고 추가적으로 준비해야되는 물건은 따로 준비해서 챙기면 매우 편리하게 짐을 준비할 수 있다. 이를 Flutter의 개념에 비추어 이해해보면, 이미 적재되어 있는 코드는 계속 현상유지를 하고 추가된 새로운 요소만 기존의 요소에 업데이트 해주는 처리만 해주면 매우 편리하고 빠르게 코드처리를 처리할 수 있다.<br>

사이즈는 전혀 문제가 되지 않는다. <br>

<strong>이번 시간에는 <font color="Blue">Container() Widget</font>에 대해서 배워볼 것이다. 이 Container() Widget은 웹의 Div태그와 같은 기능을 해준다.</strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter container widget.png" alt="blog capture" title="capture img" width="400"><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter div tag.png" alt="blog capture" title="capture img" width="400"><br>


새로운 위젯을 사용해서 개발을 할때는 항상 Flutter 공식 홈페이지의 API문서를 참조해서 만들어야 한다.<br>
<strong>이번에 배울 Container위젯은 Layout과 관련된 항목이므로, 아래 Flutter widget categories페이지에서 layout 항목을 선택한다.</strong><br>

<strong><font color="Red"> Flutter widget categories
</font></strong><br>
→ [https://flutter.dev/docs/development/ui/widgets](https://flutter.dev/docs/development/ui/widgets) <br>

<strong><font color="Red"> Flutter container widget
</font></strong><br>
→ [https://api.flutter.dev/flutter/widgets/Container-class.html](https://api.flutter.dev/flutter/widgets/Container-class.html) <br>

API의 설명을 보면 <strong>"Containers with no children try to be as big as possible"</strong>내용을 확인할 수 있다. <br>
여기에서 알 수 있듯이 Container widget에 자식 widget/container가 없다면, 컨테이너의 크기는 가능한한 커지려고 하는 속성을 가지고 있는 것을 알 수 있다.<br>

이 속성을 확인하기 위해서 Scaffold 위젯에 배경색을 넣고, body에 Container 위젯을 넣어 색상 속성을 지정해주자. 그러면 body에 넣은 Container색상으로 배경색이 모두 바뀌는 것을 알 수 있다. <br>

만약에 Container 내부에 child:Text('chlie')를 넣어주면 그 작은 텍스트만 감싸는 Container를 확인할 수 있다. <br>

<strong><font color="Red">만약에 Container를 Parent와 맞춰서 늘리고 싶다면, double.infinity 값을 height와 width의 속성에 넣어주면 된다.</font></strong><br>
<strong><font color="Blue">Container의 배경색을 바꾸기 위해서는 <font color="Red">decoration</font>과 <font color="Red">foregroundDecoration</font>을 사용해서 바꿀 수 있다. </font></strong><br>

위의 두 가지 속성을 바꿔서 Container의 모양을 완전히 바꿀 수 있다. 두 속성의 간단한 차이점을 말하자면, <strong><font color="Red">"Decoration"</font>속성은 항상 child의 뒤(Behind)에 위치한고 반면에 <font color="Red">foregroundDecoration</font>은 child의 위(Top)에 위치한다.</strong><br>

<strong><font color="Red">Container내의 배경색상 바꾸기</font></strong><br>

Way1 : use color with Color class <br>

    child: Container(
      //Set background for container.
      color: Colors.redAccent
    )

Way2 : use decoration with BoxDecoration

    return new Container(
      // This widget is the root of the application.
      decoration: new BoxDecoration(color: Colors.red),
      child: new Center(
        child: new Text("Hello, World!"),
      ),
    );

Way3 : use foregroundDecoration with BoxDecoration

    return Scaffold(
        appBar: AppBar(title: Text('Container.foregroundDecoration')),
        body: Container(
          height: double.infinity,
          width: double.infinity,
          decoration: BoxDecoration(color: Colors.yellowAccent),
          foregroundDecoration: BoxDecoration(
            color: Colors.red.withOpacity(0.5),
          ),
          child: Text("Hi"),
       ),
    );

위의 Text child를 가지고 있는 container의 위치를 확인해보면 최상단에 글자가 잘린 상태로 출력됨을 알 수 있다. 이로 인해 <strong><font color="Red">"Safe Area"</font></strong>를 설정해주면 된다.

<strong>Container 위젯에서 Alt+Enter키를 누르고 "wrap with widget"을 선택하면 Container 위젯을 감싸는 widget을 지정할 수 있다.</strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 SafeArea widget.png" alt="blog capture" title="capture img" width="400"><br>

    //Container 속성 (1)
    height: 100.0,
    width: 100.0,
    margin: EdgeInsets.all(20.0),

    //Container 속성 (2)
    height: 100.0,
    width: 100.0,
    margin: EdgeInsets.symmetric(vertical: 50, horizontal: 100),

    //Container 속성 (3)
    height: 100.0,
    width: 100.0,
    margin: EdgeInsets.fromLTRB(30.0, 10.0, 50.0, 20.0),

    //Container 속성 (4)
    height: 100.0,
    width: 100.0,
    margin: EdgeInsets.only(left: 30.0),

    //margin은 outside of widget의 간격을 조절할때 사용하고,
    //padding은 inside of widget의 간격을 조절할때 사용된다.


<strong>Flutter Inspector의 Debug Paint버튼을 이용하여 Container 위젯이 화면에서 어떻게 구성이 되어있는지 가시적으로 확인할 수 있다.</strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter debug paint.png" alt="blog capture" title="capture img" width="400"><br>

<strong><font color="Red">※ 만약에 Text 위젯 이외에 하나의 위젯을 더 넣으려고 한다면, 에러가 난다. 그 이유는 Container는 “Single-child layout widgets” 중에 하나이기 때문이다. </font></strong><br>

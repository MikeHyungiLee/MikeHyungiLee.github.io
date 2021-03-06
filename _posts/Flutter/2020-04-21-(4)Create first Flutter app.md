---
layout: post
title:  (4) Create first Flutter App
comments: true
categories: Flutter
---

## Create Flutter App

<strong><font color="Blue">이제 Flutter의 개발환경 구축이 완료되었으므로, 새로 프로젝트를 생성해서 내부 구조를 살펴볼 것이다.</font></strong><br>

이번 Posting에서는 첫 Flutter App을 만들어 볼 것이다.<br>

우선 모든 프로그래밍 공부의 기본이 되는 "Hello world!"를 어플에 띄어볼 것이다.<br>
기존에 자동생성된 class를 삭제하고, 최 상단에 있는 void main() 메소드를 수정해보자.<br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter first app capture.png" alt="blog capture" title="capture img"><br>

    void main() => runApp(MaterialApp(home: Center(child: Text('Hello World'))));

<strong>), 를 붙여주는 이유는 Formatting해서 정렬을 해주기 위해서이다.</strong><br>

To automatically format the code in the current source code window, <font color="Red">right-click in the code window and select Reformat Code with dartfmt.</font><br>

    void main() => runApp(
        MaterialApp(
          home: Center(
            child: Text('Hello World'),
          ),
        ),
    );

아래와 같이 => 를 {}로 묶어서 코드를 작성할 수도 있다.<br>

    void main(){
      runApp(
        MaterialApp(
          home: Center(
            child: Text('Hello World'),
          ),
        ),
      );
    }


<strong><font color="Blue">우선 첫번째로 살펴볼 Widget은 "Scaffold()" Widget이다.</font></strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter scaffold.png" alt="blog capture" title="capture img"><br>

<strong><font color="Red">※Flutter를 개발할때 사용될 Widget의 내용을 api문서에서 확인하며 개발하는 습관을 들여야 한다.</font></strong><br>
[Scaffold class API - official web site ](https://api.flutter.dev/flutter/material/Scaffold-class.html) <br>

<strong><font color="Blue">두번째로 살펴볼 Widget은 "AppBar()" Widget이다.</font></strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter appbar widget.png" alt="blog capture" title="capture img"><br>

이제 기존의 Center Widget을 삭제하고, 새롭게 배운 Scaffold()Widget을 넣어준다. <br>
그 다음에 Scaffold()widget의 Background속성에 색을 넣어주고, 그 안에 appBar와 body Widget을 넣어준다.<br>

결과 코드는 아래와 같다.<br>

    void main() {
      runApp(
        MaterialApp(
          home: Scaffold(
            backgroundColor: Colors.blueGrey,
              appBar: AppBar(
                title: Center(
                  child: Text("Hello World App"),
                ),
              ),
              body: Center(
                child: Image(image: NetworkImage("https://stickershop.line-scdn.net/stickershop/v1/product/8729/LINEStorePC/main.png;compress=true")),
              ),
          ),
        ),
      );
    }

위와같이 body 위젯에 이미지를 가운데 정렬하는데 사용되는 위젯은 Center Widget이다. Widget안에 또 다른 Widget을 넣을땐, child: 속성을 넣어주고, 그 안에 새로운 위젯을 넣어주면 된다.<br>
<strong><font color="Red">여기서의 핵심은 Widget안에 또 다른 Widget을 넣어줄때는 child: 속성을 이용해서 넣어준다는 것이다.</font></strong><br>

Widgets을 선택한 상태에서 Alt+Enter를 클릭하면, Widget에 적용할 수 있는 다양한 옵션들을 확인할 수 있다.<br>
"Wrap with center"를 이용해서 이미지를 가운데 정렬할 수 있다.<br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter alt enter capture.png" alt="blog capture" width="300" title="capture img"><br>

결과화면은 아래와 같다. <br>

<img src="/images/flutter/2020-04-21/2020-04-21 result screen capture(1).png" alt="blog capture" width="300" title="capture img"><br>

각 widget 클래스의 요소를 참조해가면서 코딩해야하므로, API문서에서 해당 클래스를 검색해서 확인할 수 있어야 한다.<br>
<strong><font color="Red">예를들어, 화면에 Image를 보여줘야하는 경우,</font>Image class를 검색해서 참조해야한다.</strong><br>

>>Widgets tree 그리기
> 아래의 주소를 통해서 Widgets tree를 그릴 수 있다.
> [https://www.draw.io/](https://www.draw.io/)

<img src="/images/flutter/2020-04-21/2020-04-21 widgets tree .png" alt="blog capture" width="500" title="capture img"><br>

<strong><font color="Red">※ Flutter의 developer mode</font></strong><br>
Chrome의 developer mode와 비슷하게 원반모양의 아이콘을 클릭한 후 궁금한 부분을 클릭하면 해당 부분의 요소를 트리형태로 보여준다.<br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter iOS developer mode.png" alt="blog capture" width="500" title="capture img"><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter developer mode.png" alt="blog capture" width="500" title="capture img"><br>

<strong><font color="Red">※ Debug mark 없애기.</font></strong><br>
<img src="/images/flutter/2020-04-21/2020-04-21 flutter remove debug mode.png" alt="blog capture" width="300" title="capture img"><br>

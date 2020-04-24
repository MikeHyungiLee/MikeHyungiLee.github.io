---
layout: post
title:  (16)Flutter Dice App - Expanded widget & Stateful / StatelessWidget
comments: true
categories: Flutter
---

<strong><font color="Blue">※ 레이아웃을 작성하다보면 화면상의 widget이 화면 밖으로 위치하는 경우가 생긴다.(overflow) <br>
이런 경우를 예방하기 위해 우리는 Expanded 위젯을 사용해서 레이아웃을 작성하는 것이 좋다. Expanded 위젯은 자동으로 Layout에 맞춰 화면상의 각 구성요소를 출력해주기 때문에 overflow가 발생하지 않는다.</font></strong><br>

아래 Widget tree구조를 보면 알 수 있듯이 Row 위젯의 children 요소로써 Expanded 위젯을 두 개 배치하였고, 각각의 Expanded에 FlatButton 위젯을 넣어 버튼 처리를 해주었다. 이렇게 두 개 이상의 Expanded요소를 넣고 flex 속성을 넣어주면 각 요소를 비율에 맞추어 화면에 배치할 수 있다.<br>

<strong><font color="Blue">※ 위젯을 다른 위젯의 하위에 위치시키거나 삭제 및 수정을 할때에는 <font color="Red">"Intention Action"</font>을 이용하면 widgets을 embeded하는 것이 편리하다.</font></strong><br>

<strong><font color="Red">방법1)</font></strong> 위젯을 선택하고, 안드로이드 IDE우측에 위치한 [Flutter outline] 탭을 선택, 소스코드에서 각 위젯요소를 선택시 outline의 navigator 리스트에서 해당 위젯이 선택됨을 확인할 수 있다. 이 navigator 리스트에서 우측 클릭을 해서 해당 위젯을 조작할 수 있다.<br>

<strong><font color="Red">방법2)</font></strong> 더 많은 Widget 조작을 하기 위해서는 소스코드상에서 위젯을 클릭하면 좌측에 light bulb(Intention Action) 마크가 나오는데,(Alt+Enter) 화살표를 클릭해서 다양한 Widget 조작 옵션을 활용할 수 있다. <br>

<strong><font color="Blue">※ Flutter 버튼을 활용하여 Gesture Detection을 추가해보자. </font></strong><br>

자 새로운 위젯을 사용할때에는 Widget category에서 해당 카테고리를 확인해가며 사용하도록 하자. <br>

<strong>Button Widget - FlatButton Widget Api</strong><br>

[https://api.flutter.dev/flutter/material/FlatButton-class.html](https://api.flutter.dev/flutter/material/FlatButton-class.html) <br>

다음 Api문서를 확인해보면 알 수 있듯이 FlatButton 위젯에서는 onPressed 속성과 Text 속성을 지정할 수 있다.<br>

    FlatButton(
      // Anonymous function
      onPressed: () {
        /*...*/
      },
      child: Text(
        "Flat Button",
      ),
    )

<strong><font color="Blue">※ 다음으로 알아볼 것은 Stateless Widget과 Stateful Widget의 사용이다.</font></strong><br>

<table>
  <tr>
    <th width="500">
      <strong><font color="Red">Stateless Widget</font></strong>
    </th>
    <th width="500">
      <strong><font color="Red">Stateful Widget</font></strong>
    </th>
  </tr>
  <tr>
    <td>
      <strong>if you are creating a user interface where the state of the widget isn't going to be changed.</strong><br>

      다음 설명에서와 같이 User과의  interaction에 의해 변하지 않는 화면(레이아웃)의 경우에는 Stateless Widget을 사용한다.
    </td>
    <td>
      <strong>if you are creating something which is going to be changed especially when it's dependent on user interaction.</strong><br>

      다음 설명에서와 같이 User과의  interaction에 의해 상태가 변하는 화면(레이아웃)의 경우에는 Stateful Widget을 사용한다.
    </td>
  </tr>
</table>

<strong><font color="Blue">※ StatefulWidget을 상속하는 클래스 작성하기</font></strong><br>
"stful"을 입력하면 자동으로 StatefulWidget을 상속하는 클래스와 State<T>상속하는 클래스가 자동생성된다. State<T>를 상속하는 클래스는 mutable 클래스로, 기존에 StatelessWidget상속 클래스에 작성했던 내용을 여기에 적어주면 된다.<br>

State<T> 상속 클래스에서 User의 행동으로 trigger되는 event처리하는 부분(ex. 버튼클릭)에서

    setState((){

    });

<strong><font color="Red">위의 setState를 작성해줘서 클릭이벤트가 발생했을때, build 메소드 내에 있는 코드가 다시 Re-build될 수 있도록 처리해준다. </font></strong><br>

<strong><font color="Blue">※ Dart에서 Math 라이브러리 사용하기</font></strong><br>
이번 주사위 돌리는 앱에서는 클릭할때마다 난수가 발생하여, 주사위에 표시되는 숫자가 랜덤으로 표시된다.<br>
사용법은 <strong>import 'dart:math';</strong> 라이브러리를 import하고, 코드상에서

    Random().nextInt(6)+1 // 1~6까지의 난수 발생

[https://dartpad.dartlang.org](https://dartpad.dartlang.org)<br>

<strong><font color="Red">Ref. "Dicd App Widget Tree"</font></strong><br>

<table>
  <tr>
    <td>
      <img src="/images/flutter/2020-04-23/2020-04-23 flutter dice app.png" alt="blog capture" title="capture img" width="300"> <br>
    </td>  
    <td>
      <img src="/images/flutter/2020-04-23/2020-04-23 flutter dice app widget tree.png" alt="blog capture" title="capture img" width="600"> <br>
    </td>
  </tr>
</table>

    void main() {
      return runApp(
        MaterialApp(
          home: Scaffold(
            backgroundColor: Colors.red,
            appBar: AppBar(
              title: Text('Dicee'),
              backgroundColor: Colors.red,
            ),
            body: DicePage(),
          ),
        ),
      );
    }

    class DicePage extends StatefulWidget {
      @override
      _DicePageState createState() => _DicePageState();
    }

    class _DicePageState extends State<DicePage> {
      int leftDiceNumber = 1;
      int rightDiceNumber = 1;

      void setupRandomDiceNumber(){
        setState(() {
          rightDiceNumber = Random().nextInt(6) + 1;
          leftDiceNumber = Random().nextInt(6) + 1;
        });
      }

      @override
      Widget build(BuildContext context) {
        return SafeArea(
          child: Center(
            child: Row(
              children: <Widget>[
                Expanded(
                  child: FlatButton(
                    child: Image.asset('images/dice$leftDiceNumber.png'),
                    onPressed: () {
                      // build again, re-build, re-draw
                      setupRandomDiceNumber();
                    },
                  ),
                ),
                Expanded(
                  child: FlatButton(
                    child: Image.asset('images/dice$rightDiceNumber.png'),
                    onPressed: () {
                      // build again, re-build, re-draw
                      setupRandomDiceNumber();
                    },),
                ),
              ],
            ),
          ),
        );
      }
    }

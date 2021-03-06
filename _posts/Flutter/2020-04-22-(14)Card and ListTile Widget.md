---
layout: post
title:  (14)Card and ListTile Widget
comments: true
categories: Flutter
---

<strong><font color="Blue">※ 이번 포스팅에서는 기존에 작성했던 코드를 Customized Widgets을 활용하여 간단하게 refactoring해볼것이다.</font></strong><br>

사용할 Customized widget은 <strong><font color="Red">"Card widget"과 "ListTile" Widget</font></strong>이다.<br>

일전에 MiCard App을 만들었을때, 전화와 이메일 정보를 담는 네모난 카드형태의 모양을 Container 위젯을 사용해서 구현해보았다. 하지만 앞에 아이콘이 위치하고 뒤에 그 아이콘의 타이틀이 위치하는 형태는 <strong><font color="Red">이미 Card 위젯으로 Customize되어있다.</font></strong><br>
자 그럼 두 가지 소스코드를 비교해보자.

다음 코드에서 볼 수 있듯이 Customize된 Widget을 활용하면 더욱 간단하게 소스코드를 작성할 수 있다. <br>
이전에 사용했던 <strong>CircleAvatar 위젯</strong>도 Customize Widget 중에 하나이다. 다음 소스 코드에서 Container 위젯을 Card위젯으로 바꾸었을때 <strong><font color="Red">가장 큰 변화는 padding 속성을 주는 부분</font></strong>이다.<br>
기존의 Container에서 padding을 주었을때에는 간단히 padding속성에 EdgeInsets.all(10.0) 속성을 주어 padding을 주었지만, Card 위젯을 주었을 때는 별도의 padding속성이 아닌 <strong>Padding 클래스</strong>를 사용해서 내부 위젯을 Padding위젯으로 감싸주고, 그 안에 padding 속성을 주었다.<br>

Flutter에서는 각 위젯의 구성과 전체적인 구성도에 익숙해져야 하므로, widget tree를 작성해보았다.<br>

<img src="/images/flutter/2020-04-23/2020-04-23 flutter widget tree.png" alt="blog capture" title="capture img" width="700"> <br>

위의 위젯 이외에 요소간에 경계선을 주기 위해 SizedBox 위젯 안에 Divider 위젯을 넣어 경계선을 표현해주었다.<br>

<table>
  <tr>
    <th>
      Row Widget
    </th>
    <th>
      ListTile Widget
    </th>
  </tr>

  <tr>

    <td>
    <pre>
    Container(
      padding: EdgeInsets.all(10.0),
      color: Colors.white,
      margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
      child: <b>Row</b>(
        children: <Widget>[
          Icon(
              Icons.phone,
              color: Colors.teal,
          ),
          SizedBox(
            width: 10.0,
          ),
          Text(
            '+81 80 4443 5931',
            style: TextStyle(
              color:Colors.teal.shade900,
              fontFamily: 'Source Sans Pro',
              fontSize: 20.0,
            ),
          ),
        ],
      )
    ),
  }

    <td>
      <pre>
  <b>Card</b>(
    color: Colors.white,
    margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
    child: Padding(
      padding: EdgeInsets.all(1.0),
      child: <b>ListTile</b>(
          leading: Icon(
            Icons.phone,
            color: Colors.teal,
           ),
           title: Text(
            '+81 80 4443 5931',
            style: TextStyle(
              color:Colors.teal.shade900,
              fontFamily: 'Source Sans Pro',
              fontSize: 17.0,
            ),
           ),
         ),
       ),
     ),                
      </pre>
    </td>

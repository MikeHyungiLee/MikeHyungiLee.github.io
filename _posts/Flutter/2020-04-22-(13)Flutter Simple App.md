---
layout: post
title:  (13) Flutter MiCard App
comments: true
categories: Flutter
---

<strong><font color="Blue">※ 이번 포스팅에서는 간단한 Flutter 앱을 만들어가면서 개발시에 필요한 각종 팁에 대해서 배우고, 중요한 내용들을 정리해 볼 것이다.</font></strong><br>

우선 이번에 만든 최종 앱의 모습은 다음과 같다.<br>
간단하게 Flutter로 레이아웃을 만들어 보았다. 단순한 앱이지만 레이아웃을 작성해나가면서 각 Widget을 어떻게 구성해야되는지, 여러 개념에 대해서 배울 수 있었다.<br>

빨간색으로 작성한 속성은 나중에 유용하게 사용될 수 있다고 생각이 되서, Syntax에 익숙해지기 위해서 적어두었다.<br>

<strong>※ Quick dogs의 사용 : <font color="Red">Mac에서는 Ctrl + j 단축키를</font>누르면 각 위젯에서 설정할 수 있는 속성리스트를 확인할 수 있다.</strong> <br>
<strong>Material Design에서의 Pallet와 Icons의 사용에 대해서 익숙해지자. Google에서 제공되는 유용한 디자인 도구이므로, 잘 활용할 수 있도록 연습을 하자.</strong><br>

[https://material.io/](https://material.io/)<br>

<strong>이번 Flutter 앱을 만들어보면서 Container에 padding과 margin속성을 주는 작업을 하였는데, <font color="Red">EdgeInsets.all, EdgeInsets.symmetric 등 EdgeInsets를 이용해서 padding과  margin값을 지정할 수 있다는 것을 배웠다.</font></strong><br>

<table>
  <tr>
    <td>
      <img src="/images/flutter/2020-04-23/2020-04-23 flutter micard app capture.png" alt="blog capture" title="capture img" width="300"> <br>
    </td>
    <td>
      <img src="/images/flutter/2020-04-23/2020-04-23 micard widget tree diagram.png" alt="blog capture" title="capture img" width="1000"> <br>
    </td>
  </tr>
</table>

    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        return MaterialApp(
          home: Scaffold(
            backgroundColor: Colors.teal,
            body: SafeArea(
              child: Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: <Widget>[
                    CircleAvatar(
                      radius: 50.0,
                      backgroundColor: Colors.red,
                      backgroundImage: AssetImage('images/profile picture.jpg'),
                    ),
                    Text(
                      'Lee Hyungi',
                      style: TextStyle(
                        fontFamily: 'Pacifico',
                        fontSize: 40.0,
                        color: Colors.white,
                        fontWeight: FontWeight.bold,
                      ),
                    ),
                    Text(
                      'Flutter Developer',
                      style: TextStyle(
                        fontFamily: 'Source Sans Pro',
                        color: Colors.teal.shade100,
                        fontSize: 20.0,
                        letterSpacing: 2.5,
                        fontWeight: FontWeight.bold
                      ),
                    ),
                    Container(
                      padding: EdgeInsets.all(10.0),
                      color: Colors.white,
                      margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                      child: Row(
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
                    Container(
                      padding: EdgeInsets.all(10.0),
                      margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                      color: Colors.white,
                      child: Row(
                        children: <Widget>[
                          Icon(
                            Icons.email,
                            color: Colors.teal,
                          ),
                          SizedBox(
                            width: 10.0,
                          ),
                          Text(
                            'mike.hyungi.lee@gmail.com',
                            style: TextStyle(
                              color: Colors.teal.shade900,
                              fontSize: 20.0,
                              fontFamily: 'Source Sans Pro',
                            ),
                          )
                        ],
                      ),
                    ),
                  ],
                ),
              ),
            ),
          ),
        );
      }
    }

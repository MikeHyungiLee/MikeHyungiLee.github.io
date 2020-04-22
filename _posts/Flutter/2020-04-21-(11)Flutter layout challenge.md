---
layout: post
title:  (11) Flutter layout challenge
comments: true
categories: Flutter
---

<strong><font color="Blue">※ Flutter challenge layout & layout diagram</font></strong><br>

<table>
  <tr>
    <td>
      <img src="/images/flutter/2020-04-22/2020-04-22 flutter layout capture.png" alt="blog capture" title="capture img" width="350"><br>
    </td>
    <td>
      <img src="/images/flutter/2020-04-22/2020-04-22 flutter challenge diagram.png" alt="blog capture" title="capture img" width="800"><br>
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
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.spaceBetween,
                  crossAxisAlignment: CrossAxisAlignment.stretch,
                  children: <Widget>[
                    Container(
                      width: 100.0,
                      color: Colors.red,
                      child: Text('Container1'),
                    ),
                    Container(
                      width: 100.0,
                      child: Column(
                        mainAxisAlignment: MainAxisAlignment.center,
                        mainAxisSize: MainAxisSize.min,
                        children: <Widget>[
                          Container(
                            width: 100,
                            height: 100,
                            color: Colors.yellow,
                          ),
                          Container(
                            width: 100,
                            height: 100,
                            color: Colors.green,
                          ),
                        ],
                      ),
                    ),
                    Container(
                      width: 100.0,
                      color: Colors.blue,
                      child: Text('Container2'),
                    ),
                  ],
                ),
            ),
          ),
        );
      }
    }

<strong><font color="Red">Flutter app layout diagram</font></strong><br>
이번 Challenge로 만든 레이아웃을 다른 구조로 Diagram 툴로 그려보았다.<br>

<table>
  <tr>
    <td>
      <img src="/images/flutter/2020-04-22/2020-04-22 flutter layout captrue(2).png" alt="blog capture" title="capture img" width="350"><br>   
    </td>
    <td>
      <img src="/images/flutter/2020-04-22/2020-04-22 flutter layout diagram.png" alt="blog capture" title="capture img" width="600"><br>
    </td>
  </tr>
</table>  

    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        const iconSize = 50.0;
        return MaterialApp(
          home: Scaffold(
            backgroundColor: Colors.teal,
            body: Row(
              children: <Widget>[
                Expanded(
                  child: SafeArea(
                    child: Container(
                      decoration: const BoxDecoration(color: Colors.red),
                    ),
                  ),
                  flex: 1,
                ),
                Expanded(
                    child: Center(
                      child: Column(
                        mainAxisSize: MainAxisSize.min,
                        children: <Widget>[
                          Container(
                            color: Colors.yellow,
                            width: 100.0,
                            height: 100.0,
                          ),
                          Container(
                            color: Colors.green,
                            width: 100.0,
                            height: 100.0,
                          )
                        ],
                      ),
                    ),
                    flex: 3
                ),
                Expanded(
                  child: SafeArea(
                    child: Container(
                      decoration: const BoxDecoration(color: Colors.blue),
                    ),
                  ),
                  flex: 1,
                ),
              ],
            ),
          ),
        );
      }
    }

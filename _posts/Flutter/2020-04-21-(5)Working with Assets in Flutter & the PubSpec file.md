---
layout: post
title:  (5)Working with Assets in Flutter & the PubSpec file
comments: true
categories: Flutter
---

## Flutter app에 이미지 넣어주기 <br>

Project에 Images 폴더를 만들어서 이미지 파일을 넣어줄 것이다.<br>

<strong>① 프로젝트 폴더의 바로 아래에 <font color="Red">"images"</font>폴더를 만들어준다.</strong><br>

<strong>② pubspec.yaml 파일에 새로 만든 <font color="Red">assets폴더의 경로를 지정</font>해준다.</strong><br>

특정 파일만 지정을 안해주고 - image/ 디렉토리 경로만 설정해줘도 폴더 안에 모든 파일을 읽는데 문제가 되지 않는다.<br>

<img src="/images/flutter/2020-04-21/2020-04-21 pubspec yamal file.png" alt="blog capture" title="capture img"><br>

<strong>assets의 요소를 보면 flutter: (Parents)의 자식으로 구성되어있는 것을 확인할 수 있다.</strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 yaml language.png" alt="blog capture" title="capture img"><br>

<strong><font color="Blue">yaml 언어는 들여쓰기에 주의해서 작성을 해주어야 한다.</font></strong><br>

③ 모든 설정이 끝난다음에는 <strong>"Packages get"을 눌러서 프로젝트에 적용</strong>시켜준다.<br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter configuration change.png" alt="blog capture" title="capture img"><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter app.png" width="300" alt="blog capture" title="capture img"><br>

이 화면에 보여지는 이미지는 해상도별로 나눠서 단말기에 넣어주지 않으면 안된다. <br>
각 단말기별로 해상도가 다르므로, 화면에 이미지가 출력이 될때 해상도를 고려해서 화면에 출력을 해주어야 한다.<br>

<strong><font color="Red">※ Icon 이미지를 해상도별로 나눠주는 웹 Generator : </font></strong>[https://appicon.co](https://appicon.co) <br>

<img src="/images/flutter/2020-04-21/2020-04-21 image generator.png" width="300" alt="blog capture" title="capture img"><br>

iPhone과 Android앱에 맞추어 App의 아이콘을 추출할 수도 있다.<br>

<img src="/images/flutter/2020-04-21/2020-04-21 asset folder location.png" width="300" alt="blog capture" title="capture img"><br>

Android / iOS는 각각 Asset folder의 위치가 다르므로 위의 위치를 고려해서 이미지를 넣어주어야 한다.<br>

아이콘 이미지를 import시켜주었다면 실 단말기 화면에 보여질 App의 Icon이미지를 만들어주어야 한다.<br>
이전에 안드로이드 작업을 하면서 알게 된 것인데, 단말기의 기종마다 어떤 기종은 아이콘 이미지를 원으로 만들어서 출력하는 기종도 있고, 어떤 기종은 네모난 모양으로 만들어서 아이콘 이미지에 보여주는 것도 있었다. 이러한 점을 개선하기 위해서 아래의 작업을 해준다.<br>

<strong><font color="Red">[res] - "Right click" - [new] - "Image Assets"</font></strong><br>

<img src="/images/flutter/2020-04-21/2020-04-21 android image asset.png" width="600" alt="blog capture" title="capture img"><br>

<img src="/images/flutter/2020-04-21/2020-04-21 flutter app img.png" width="300" alt="blog capture" title="capture img"><br>

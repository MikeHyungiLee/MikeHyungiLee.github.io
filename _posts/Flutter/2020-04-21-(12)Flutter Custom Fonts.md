---
layout: post
title:  (12) Flutter Custom Fonts
comments: true
categories: Flutter
---

<strong><font color="Blue">※ 이번 포스팅에서는 Flutter 앱에 Custom Fonts를 import하는 방법에 대해서 알아 볼 것이다.</font></strong><br>

<strong>우선 Google에서 제공하는 Custom fonts 다운로드 사이트는 아래와 같다.</strong><br>

[fonts.google.com](fonts.google.com)

위에 사이트에서 *.ttf 확장자의 파일을 다운받는다.<br>

다운받은 font들은 프로젝트 최상위 위치에 'fonts'폴더를 만들어서 복사붙여넣기 해준다.<br>
그 후에는 <strong><font color="Red">"pubspec.yaml"</font></strong> 안에 아래의 fonts폴더의 위치를 잡아준다.(이 과정은 이전에 배웠던 images 폴더를 추가하고 프로젝트에 적용시켰던 작업과 동일하다)<br>

    fonts:
       - family: Pacifico
         fonts:
           - asset: fonts/Pacifico-Regular.ttf

       - family: Source Sans Pro
         fonts:
           - asset: fonts/SourceSansPro-Regular.ttf
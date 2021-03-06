---
layout: post
title:  (6) Running your app on a physical device
comments: true
categories: Flutter
---

### Deploying Your Flutter Apps to a Physical Device <br>

<strong><font color="Blue">실제 안드로이드 단말기에서 Flutter App을 deploy하는 방법을 살펴보자.</font></strong>

우선 아래의 순서대로 실제 안드로이드 단말기에서 설정해준다.<br>

(1) [About] - Software Information - Build number (need to tap the menu until being developer mode.)<br>
(2) Enable USB Debugging<br>
(3) Connect Your Phone with USB<br>
(4) Set “Trust Connected PC”<br>

※ TroubleShooting Reference<br>
[https://blog.londonappbrewery.com/troubleshooting-android-device-testing-on-windows-a2b5d779df08](https://blog.londonappbrewery.com/troubleshooting-android-device-testing-on-windows-a2b5d779df08) <br>

<strong><font color="Blue">실제 iOS 단말기에서 Flutter App을 deploy하는 방법을 살펴보자.</font></strong>

아래의 Requirements를 우선준비한다.<br>
>Requirements
>>① An Apple ID 준비하기<br>
>>② An iPhone/iPad Device <br>
>>③ Xcode 설치 <br>
>>④ USB Cable <br>

>><strong><font color="Green">iOS 실 단말기에 Flutter app을 deploy하기 위한 5 Steps</font></strong> <br>

>① <strong><font color="Red">iOS버전이 Xcode 버전과 호환이 되는지 확인하기</font><br>
iOS의 소프트웨어 버전 = 12.3이라고 가정하면, 우선 소수점 앞자리 12에서 2를 빼서(12-2) 10이라는 숫자가 된다.<br>
실제 내 단말기를 확인하면, 13.3.1 버전이고 소수점 맨 앞자리 13에서 2를 빼면(13-2) 11이라는 숫자가 된다. <br>
위에서 계산된 숫자는 Xcode의 최소로 요구되는 버전가 된다.<strong>Xcode는 최소 버전 11이어야 하고, 동시에 두번째 숫자는 Xcode버전의 두번째 숫자보다 작거나 같아야 한다.</strong><br><font color="Red">내가 설치한 Xcode버전은 11.3.1 / iOS버전은 13.3.1이므로 위의 두 조건을 모두 만족한다.</font><br>만약에 버전이 일치하지 않는다면, Xcode의 버전을 업그레이드 하는 것이 최선이다. <br>
MacOS 버전이 업데이트 되었다면, Xcode 버전도 함께 업데이트하자.<br>

>② homebrew를 설치한다. <br>
[https://brew.sh/index_ja](https://brew.sh/index_ja)<br>
<strong>/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)”</strong><br>
<strong><font color="Red">Use home-brew to install ideviceInstaller, iOS-deploy & cocoa pods</font></strong><br>
아래 링크의 "Deploy to iOS devices"를 참조해서 설치하기<br>

>③ Xcode에서 "Apple ID"를 등록하기<br>
<strong>(1) 프로젝트에서 iOS module in Xcode를 이용해서 Xcode열기</strong>
<img src="/images/flutter/2020-04-21/2020-04-21 flutter xcode open.png" alt="blog capture" title="capture img"><br>
<strong>(2) Xcode에서 [Runner] - [Targets App을 선택] - [Signing & Capabilities 탭을 선택] - All - [Add Account]
내 Apple ID로 로그인한 뒤에 Develop Team 선택하기.</strong>
<img src="/images/flutter/2020-04-21/2020-04-21 flutter apple id register.png" alt="blog capture" title="capture img"><br>
<img src="/images/flutter/2020-04-21/2020-04-21 flutter regeister apple id.png" alt="blog capture" title="capture img"><br>

>④ 실제 iOS단말기를 USB로 연결하고, "Trust connected Computer" 선택하기<br>
<strong><font color="Red">만약에 앱이 단말기에 기동되지 않는다면, 신뢰된 App으로 인식이 안되서 앱이 기동이 되지 않는 것이다.</font></strong><br>
[General] - Device Management - Click the App  - check - Trust Profile and device management - developer app 아래에 어플 설정 들어가서 Trust클릭! - Create Unique bundle ID<br>

>⑤ 최종적으로 Android studio에서 Flutter를 진단해본다.<br>
Android studio - [final check] - Flutter doctor<strong><font color="Red"> (Check the setup process)</font></strong><br>
※ iOS에 앱을 기동시켰을때 에러가 나는 경우, 아래 troubleshooting페이지를 확인하자.<br>
[https://blog.londonappbrewery.com/troubleshooting-ios-device-testing-for-flutter-38c5da239e62](https://blog.londonappbrewery.com/troubleshooting-ios-device-testing-for-flutter-38c5da239e62) <br>

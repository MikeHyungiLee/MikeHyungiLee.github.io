---
layout: post
title:  Tests in Android
categories: Android
comments: true
---

<strong>안드로이드에는 어떤 종류의 테스트가?</strong><br>
총 세가지의 테스트 종류가 있다.<br>
① Local Unit Tests  
② Instrumentation Tests  
③ UI Test  
<img src="/images/android/2020-04-10 android test.png" alt="blog capture" width="500" title="capture img"><br>

우선 <strong>Local Unit Tests<strong>에 대해서 살펴보자<br>  

>①Local Computer<br>
>② Java Virtual Machine(JVM)<br>
>③ Very fast (not required to use emulator, run raw java code, sequence of method, logic based test)<br>  
>(Local Unit Tests는 별도의 emulator를 사용하지 않고, logic을 베이스로 java코드를 실행해서 하는 테스트이기 때문에 속도가 매우 빠르다)<br>
>④ JUnit5, Mockito<br>  

그 다음으로 살펴볼 것은 <strong>Instrumentation Tests</strong>이다.<br>  

>① Similar to local unit tests(Local Unit Tests와 매우 유사하지만, 조금 다르다)<br>
>② Test Android functionality (Activity, Fragment, Services Life cycle) 검사 목적의 테스트<br>
>③ Need a real device or emulator - framework<br>
>④ JUnit4, Mockito<br>

마지막으로 살펴볼 테스트는 <strong>UI테스트</strong>이다.<br>

>① Simulate a person using your app<br>
>② Literally uses widgets<br>
>   (Pressing a button, entering a text)<br>
>③ Real device or emulator<br>
>④ Expresso Library<br>  

<table>
  <tr>
    <td>
      <img src="/images/android/2020-04-10 Android Test folder.png" alt="blog capture" width="500" title="capture img"><br>
    </td>
    <td>
      안드로이드 스튜디오에서 Project view로 전환하면 좌측의 폴더구조와 같이 androidTest, main, test폴더를 볼 수 있다.<br>
      우선 첫번째 androidTest 폴더의 경우, Instrumentation Tests와 UI 테스트를 하는 곳으로, Mockito, JUnit과 Expresso 라이브러리를 사용한다. <br>
      두번째 test폴더의 경우, Local Unit Tests를 하는 곳으로, Mockito와 JUnit 라이브러리를 사용한다.
    </td>
  </tr>
</table>
<br>
## Professional Unit Tests!
>새로운 Java component<br>
>① ViewModels<br>
>② Room Persistence<br>
>③ Repository(MVVM)<br>
>④ 'Local' Unit Testing<br>

JUnit5 - 새로운 Junit 라이브러리<br>

JUnit4 - 일부 라이브러리와 호환이 되지 않는 경우가 있다.

Mockito - Third part library이지만 대부분의 회사에서 사용되고 있는 라이브러리이다.<br>
Fake class! Mocks of objects (Fake objects) - Network request test, MVVM request, Repository server HTTP request, <br>
mock the class and certain 조건에 따른 데이터 처리 테스트를 해볼 수 있다.<br>

<strong>Testing with AndroidX</strong><br>
① Room Database<br>
② Room DAO<br>
③ ApplicationProvider<br>
④ Instant TaskExecutorRule<br>

<strong>Test-driven Development(TDD)</strong><br>
① Implement feature<br>
② Unit test feature<br>
③ Implement feature<br>
④ Unit test feature<br>
⑤ Repeat...<br>

## Local Unit Tests  

---
layout: post
title:  Java MVVM Part7 ~ 9
categories: Android-Architecture
comments: true
---

<strong>#7 Android MVVM Architecture Tutorial - Handling API Exceptions<br></strong>

<strong>참고</strong>:[https://www.youtube.com/watch?v=67bdklHmXA8&list=PLk7v1Z2rk4hjVaZ8DZKe8iT9RIM9OUrwp&index=1](https://www.youtube.com/watch?v=67bdklHmXA8&list=PLk7v1Z2rk4hjVaZ8DZKe8iT9RIM9OUrwp&index=1)<br>

API 송수신 에러를 처리를 구현해 볼 것이다. <br>


※ 노트정리 (Part7)<br>
<img src="/images/android/2020-04-20/2020-04-20 Handling API Exceptions.png" alt="blog capture" width="500" title="capture img"><br>

ViewModel클래스에서 호출해서 사용할 UserRepository의 메소드를 살펴보자. 이 메소드는 기존에 Response 객체를 반환하고, 이 반환된 객체를 ViewModel에서 일일이 송수신 성공여부(로그인 성공/실패)에 따라서 이벤트 처리를 해주었다. <br>
<strong><font color="Red">하지만 이런식으로 반복해서 ViewModel 클래스에서 매번 조건처리해서 적어주면 코드의 가독성이 떨어지기 때문에, 이러한 처리를 공통화 처리해주기로 한다.</font></strong><br>

위의 공통화 처리해서 작성해줄 부분이 network 패키지 아래에 작성한 SafeApiRequest 추상클래스이고, 여기에서 작성한 메소드는 송수신 성공시에는 ResponseBody를 반환해주고, 실패하면, 에러 메시지를 덫붙여서 ApiException 클래스에 던져준다. <br>

    class ApiException(message: String) : IOException(message) {

    }

위와 같이 IOException클래스를 상속하고, String타입의 message 변수를 인자로 갖는 ApiException클래스를 작성해서 활용한다. 이 ApiException 클래스는 IOException의 기능을 계승한다.<br>

<strong>이렇게 작성을 하게 되면, 최종적으로 AuthViewModel 클래스에서 Repository클래스 내부에서 작성한 메소드로 값을 반환할때, <font color="Red">try{}catch{}내에서 커스터마이징한 ApiException클래스로 송수신 성공/실패를 에러로써 Catch해서 처리할 수 있게 된다.</font></strong><br>

이 부분은 연습이 필요할 것 같다.<br>
  
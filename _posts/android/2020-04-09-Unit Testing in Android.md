---
layout: post
title:  Android Unit Testing
categories: Android
comments: true
---

실제로 Test case를 작성해가면서, Unit Test를 해 볼 것이다.<br>
~(test)Package는 안드로이드 기능과 상관없는 'Java' 혹은 'Kotlin'코드를 테스트할 수 있다.<br>
~(androidTest)Package는 안드로이드 환경과 연고나된 코드를 테스트 할 수 있다. - 안드로이드 환경에서 테스트하는 것이기 때문에, 에뮬레이터나 안드로이드 기기가 필요하다.<br>

기본적으로 Unit Test를 테스트하는 곳은 ~(Test)Package에서 작업을 한다.<br>
<strong><font color="Red">'단위(Unit)테스트'는</font></strong><br>

① 보통 위 경우와 같이 예측과 실제 결과를 비교합니다. 과학 실험과 비슷하게 '가설'을 세우고, '각종 변인들을 통제'한다.이후에 실험의 결과가 가설의 예측 결과와 동일한지 확인을 한다.<br>

② 복잡한 소프트웨어를 작은 모듈로 분리하여, 코드가 정상적으로 동작하는지 확인한다. <br>

③ 테스트를 빠르게 수행할 수 있다.<br>

※ 하지만, "필요한 경우에 단위 테스트를 하되, 모든 기능에 대한 단위 테스트를 반드시 해야할 필요는 없다." 그 이유는 종종 단위테스트에 너무 신경을 쓴 나머지, 프로그램이 구현해야 하는 중요한 비즈니스 로직보다 테스트를 위해서만 존재하는 코드들을 위해 많은 시간을 투자해야 되는 경우도 있기 때문이다.<br>

### <strong>테스트 방법론</strong>(Test-Driven Development : <strong>TDD</strong>) <br>
'테스트 주도 개발' 등 테스트 방법론에서는 실제 로직에 해당하는 코드를 작성하기 전에 테스트 코드부터 만들 것을 권장한다.<br>
가령 테스트 주도 개발에서는 먼저 테스트를 만드고 실패한 뒤, <strong><font color="Red">먼저 작성한 테스트 코드를 통과 가능한 코드로 만드는 방식으로 개발을 진행</font></strong>한다. <br>
이 방법은 저번 운용보수 겐바에서 뉴스 어플의 batch처리를 수정하는 현장에서 일을 했을때, 단위테스트를 하면서 에러가 발생한 조건이 있다면, 이 조건에러없이 통과 가능하도록 기존의 코드를 수정하는 방식으로 진행했었는데, 이 방식이 바로 TDD(Test-Driven Development)방식이다.<br>

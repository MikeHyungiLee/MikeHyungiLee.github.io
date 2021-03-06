---
layout: post
title:  Java and Kotlin
categories: Android
comments: true
---

### Java와 Kotlin 클래스의 차이점<br>
① 코들린 클래스와 Java 클래스의 차이점 중 하나는 코틀린은 'Getter, Setter'가 자동 생성된다.<br>
② 코틀린 클래스에서 'var'로 선언한 변수는 getter,setter 전부 생성되고, 'val'키워드로 선언된 변수는 getter만 선언된다.<br>
③ 코틀린에서 field변수에 대한 setter method를 customize해서 사용해야 되는 경우가 있는데, 이 경우에는 다음과 같이 <br>

    var nickName = ""
        set(value){
          field = value.toLowerCase()
        }

위와 같은 문법을 사용하는 이유는 'Property의 이름'을 사용하는 경우, 자동으로 Setter, Getter가 호출되기 때문이다. <br>
접근자(Getter, Setter)에서 field키워드로 사용되는 개념을 'Property를 뒷받침하는 field'라는 의미의 'Backing Field'라 불린다.<br>
Kotlin에서는 field를 사용하지 않기 때문에 이렇게 field키워드를 사용해서 접근한다.

Property의 위임은 코틀린이 객체의 Property를 더욱 유연하게 활용할 수 있도록 지원하는 기능 <br>

### Property와 Field의 차이점 <br>
코틀린은 기본적으로 Field를 사용하지 않는다.<br>

Field는 클래스에 선언되어 있는, '클래스 변수'가 아닌 '인스턴스 변수'를 의미한다.<br>
필드는 외부에서 접근할 수 있는 Getter, Setter 메소드가 반드시 존재할 필요가 없다.따라서 Getter, Setter는 있건 없건 상관없다.<br>

클래스의 인스턴스 변수들을 모두 Field라고 부릅니다. Getter, Setter가 있든 없든, 혹은 접근 제어자가 무엇이든 Field이다. <br>

<strong><font color="Red">반면, Property는 조금 다르다!</font></strong><br>
① Field가 선언되어 있고 Getter, Setter가 있는 경우 Property이다.<br>
② Getter만 선언되어 있어서, 변수의 값을 읽을수만 있는 경우도 Property이다.<br>
③ 단순 Field는 Property가 아니다. <strong>ex) private int notProperty1 = 0;</strong><br>
④ 클래스 변수 역시 Property가 아니다. <strong>ex) private static int notProperty2;</strong> <br>

※ Property는 Field와 외부에서 접근 가능한 Getter 또는 Setter가 있는 경우이다. 더 정확히 말하면 Property는 Field와 접근 가능한 Getter, Setter의 조합을 의미한다.<br>

코틀린은 기본적으로 클래스의 상속을 불가능하다. <br>
이렇게 만든 이유는 Java분야의 유명서적 'Effective Java'에서는 상속에 대하여 '상속을 위한 설계와 문서를 갖추거나, 그렇지 않은 경우 상속을 금지하라'라고 조언한다. <br>
캡슐화의 주요 목적 중 하나는 클래스를 사용하는 측면에서 해당 클래스의 구체적인 사항을 모르게 하는 것입니다. 하지만, 구체적인 구현 클래스를 알고 있는 상태에서 구현해야하는 상황이 발생한다면, 이는 "캡슐화가 깨졌다"라고 볼 수 있다.<br>
Kotlin에서 상속을 허용하려면, 'open'키워드를 사용해야 한다.<br>
코틀린에서 클래스의 메소드는 기본적으로 'final'상태이기 때문에, 클래스뿐만 아니라 메소드 역시 open처리를 해야 override할 수 있다!<br>
Override하는 함수에 대해서는 반드시 'override'키워드를 사용해야만 한다.<br>

# '위임' : 코틀린에서 상속의 단점을 줄이고 코드를 재사용할 수 있다.<br>
### 클래스와 프로퍼티의 위임<br>
<strong><font color="Blue">객체 지향에서 위임이란?</font></strong><br>
클래스의 특정 기능들을 대신 처리해 주는 것을 말한다.<br>

<strong>클래스를 상속하지 않고 기존 클래스의 일부 메소드를 변경하거나 새로운 기능을 확장하는 방법은 '위임'이다. </strong><br>
<strong>위임을 사용하는 대표적인 패턴에는 <font color="Red">데코레이터(Decorator)패턴</font>이 있다.</strong><br>

<strong><font color="Red">'데코레이터 패턴'</font></strong>은 그 이름처럼 특정 클래스의 기능에 추가 기능을 덧붙이는 방법이다.<br>
<strong>'기존에 설계된 객체에서 책임을 전달하는 것'</strong>이 '위임'입니다. 확장 기능은 자신이 실행하고, 기존의 기능은 그대로 기존 객체의 메소드에 전달하는 방식이다.<br>

데코레이터 패턴은 이런 위임을 활용한 패턴 중 하나로, 보통 기존 기능에 추가 기능을 덧붙이는 패턴이다. 데코레이터 패턴을 활용하면 기존 클래스를 상속받지 않은 상태로 새로운 추가 기능을 덧붙이거나 확장할 수 있다.<br>

문제는 이런 Decorator 패턴의 경우, 단순한 경우에도 코드가 상당히 길어진다는 것이다. 인터페이스에 포함된 메소드가 많다면 코드가 매우 길어진다. 그 이유는 일단은 인터페이스의 모든 메소드를 구현해야 한다.<br>

코틀린은 클래스 위임을 언어 차원에서 제공하기 때문에, 훨씬 간결하게 표현할 수 있다.<br>
<strong>ex)</strong> 'by' 명령어를 이용해서 인터페이스의 기능을 위임<br>
class DelegatingArrayList<T>(private val innerList: MutableCollection<T> = mutableListOf()) : MutableCollection<T> by innerList<br>

→ 위의 코틀린 코드는 'innerList'라는 ArrayList타입의 Property가 있고, 'Collection'인터페이스를 상속받고, <strong><font color="Red">Collection 인터페이스의 기능을 'innerList'에 위임</font></strong>하겠다"는 의미이다.<br>

<strong><font color="Blue">프로퍼티 위임이란?</font></strong><br>
코틀린에서는 '클래스'뿐만 아니라 '프로퍼티'에 대해서도 '위임'을 제공한다. 코틀린의 '프로퍼티 위임'은 Getter, Setter 연산자를 위임할 수 있게 해준다.<br>
방법으로는 아래 세 가지 방법이 있다.<br>

① Lazy 위임 : 프로퍼티의 초기화를 인스턴스 생성 시점이 아니라 프로퍼티를 사용하는 시점에 초기화하는 것 <br>
  <strong>→ 인스턴스 생성 시점에 모든 초기화를 진행한다면 전체적인 성능이 매우 저하된다. 그래서 일단은 초기화를 하지 않고 사용하다가 실제로 사용하는 시점에 초기화를 하는 것을 '게으른 초기화(lazy initialization)'라 하며, 프로그래밍에서 자주 사용되는 패턴 중 하나이다.</strong><br>

  ※ lateinit과 lazy는 게으른 초기화를 위해 사용한다는 측면에서 동일하지만, 그 외 특징은 꽤 다르다. <br>
  (1) lateinit은 lazy처럼 위임이 아닌 변수의 <strong>변경자(modifier)</strong>로 사용한다. <br>
  변경자(modifier)란? 변수의 성질을 변경하는 것인데, 'private, public, static, final'등도 모두 변경자이다. lateinit은 나중에 변수가 초기화될 것임을 표시하는 것이다. <strong>"이 프로퍼티는 이후 초기화되어 null이 아닐 것이 확실하니, 사용할때 null을 신경쓰지 않고 사용하겠다" 라고 컴파일러에게 알려주는 것이다.</strong><br>

② <strong>Observable 위임</strong> : 주로 관찰하고자 하는 대상에 변경 사항이 생길 때, 변경된 사실을 관측자에게 알려주는 것이다.<br>

③ <strong>프로퍼티를 Map 객체에 위임</strong> : 특정 Key에 해당하는 Value를 저장<br>

### Singleton 패턴 및 Object 클래스<br>

Singleton 패턴 : 한 개의 인스턴스 생성을 보장하고, 코드 어디에서나 접근 가능하게 하는 것이다.<br>

<table>
  <tr>
    <td width="500">
      <b>자바에서의 Singleton class</b>
    </td>
    <td width="500">
      <b>코틀린에서의 Singleton class</b><br>
      어차피 싱글턴 패턴은 거의 뻔한 코드를 사용하는 것이므로, 그냥 키워드로 제공한다. 단순히 object 키워드를 사용하는 것만으로 Java에서 꽤 복잡하게 작성한 코드들을 생략가능하다.
    </td>
  </tr>
  <tr>
    <td>
      <img src="/images/android/2020-04-11 SingletonJava.png" alt="blog capture" width="500" title="capture img"><br>
    </td>
    <td>
      <img src="/images/android/2020-04-11 Singleton Kotlin.png" alt="blog capture" width="500" title="capture img"><br>
    </td>
  </tr>
</table>

### Data 클래스 <br>

Kotlin에서는 'toString()', equals(), hashCode()'등의 함수를 자동으로 생성해주는 'Data'클래스를 지원한다. <br>

### 클래스의 가시성 변경자 <br>

클래스에서 '가시성 변경자'는 클래스의 메소드 혹은 필드에 대해 접근을 허용하는지 결정하는 역할을 한다.<br>
'private, protected, default, public' 키워드로 사용했던 '접근 제어자'와 같은 의미한다. 먼저 Java의 가시성 변경자와 의미에 대해서 알아보자. <br>

<strong>자바의 가시성 변경자(접근 제어자)</strong><br>
<table>
  <tr>
    <td>
      변경자
    </td>
    <td>
      의미
    </td>
  </tr>
  <tr>
    <td>
      default(기본 가시성)
    </td>
    <td>
      같은 패키지에서 접근 가능
    </td>
  </tr>
  <tr>
    <td>
      private
    </td>
    <td>
      클래스 내부에서만 사용 가능하며 외부에 비공개
    </td>
  </tr>
  <tr>
    <td>
      protected
    </td>
    <td>
      클래스와 상속받은 하위클래스에서만 사용 가능
    </td>
  </tr>
  <tr>
    <td>
      public
    </td>
    <td>
      외부에서 모두 접근 가능
    </td>
  </tr>
</table>
<br>
<strong>코틀린의 가시성 변경자</strong><br>
코틀린에서는 함수나 프로퍼티가 꼭 클래스 내부에만 존재하는 것이 아니기 때문에 의미가 추가된다. '클래스 멤버일 때'의 의미와 '최상위 선언인 경우' 그 의미가 조금 다르다. <br>

<table>
  <tr>
    <td>변경자</td>
    <td>클래스 멤버</td>
    <td>최상위 선언</td>
  </tr>
  <tr>
    <td>internal</td>
    <td>같은 모듈에서 접근 가능</td>
    <td>같은 모듈에서 접근 가능</td>
  </tr>
  <tr>
    <td>private</td>
    <td>클래스 내부에서만 사용 가능하며, 외부에 비공개</td>
    <td>같은 파일에서만 접근 가능</td>
  </tr>
  <tr>
    <td>protected</td>
    <td>클래스와 상속받은 하위 클래스에서 사용 가능</td>
    <td>최상위 선언에서는 사용 불가</td>
  </tr>
  <tr>
    <td>public(기본 가시성)</td>
    <td>모든 곳에서 접근 가능</td>
    <td>모든 곳에서 접근 가능</td>
  </tr>
</table><br>
Java와 달리 코틀린은 같은 패키지에서 접근 가능한 'default' 속성이 따로 없다. 대신에 <strong><font color="Red">같은 모듈일때 접근 가능한 변경자로써 'internal' 키워드</font></strong>가 있습니다.<br>
여기서 <strong><font color="Red">모듈이란?</font></strong> 무엇인가. 모듈은 <strong><font color="Red">한꺼번에 컴파일되어 묶이는 하나의 프로젝트 단위</font></strong>라고 볼 수 있다. 현재 안드로이드 프로젝트를 기준으로 한다면 <strong><font color="Red">개별 'app'이 바로 '모듈의 단위'</font></strong>라고 할 수 있다.<br>

### 내부 클래스와 중첩 클래스<br>

<table>
  <tr>
    <td></td>
    <td>Java</td>
    <td>Kotlin</td>
  </tr>
  <tr>
    <td>내부 클래스</td>
    <td>
      클래스 내부에 선언된 클래스를 내부 클래스(Inner Class)라고 한다.<br>
      내부 클래스는 외부로 선언된 외부 클래스 객체가 생성되어야 존재할 수 있다.<br>
      내부 클래스에서는 외부 클래스의 필드에 접근 가능하다.<br>
    </td>
    <td>
      코틀린은 내부 클래스를 선언하려면 inner 키워드를 사용하면 된다.<br>
      내부 클래스에서는 외부 클래스의 속성에 접근 가능하다.<br>
    </td>
  </tr>
  <tr>
    <td>중첩 클래스</td>
    <td>
      클래스 내부에 선언되어 있지만 static이 붙으면 중첩 클래스가 된다.<br>
      중첩 클래스는 외부에 있는 외부 객체가 없어도 존재할 수 있다.<br>
      중첩 클래스는 외부 클래스 필드에 접근이 불가하다.<br>
    </td>
    <td>
      코틀린은 내부에 클래스를 선언하면 중첩클래스가 된다.<br>
      중첩 클래스에서는 외부 클래스 속성에 접근 불가하다.<br>
    </td>
  </tr>
</table>
<br>
### 전체적인 학습내용을 복습한다.<br>
1. 코틀린에서 클래스의 프로퍼티는 val의 경우 Getter가, var의 경우 Getter, Setter가 자동 생성된다.<br>
2. 필드란 '인스턴스 변수'를 의미하고 프로퍼티란 '필드와 접근자(Getter, Setter)의 조합'을 의미한다.<br>
3. 코틀린의 프로퍼티는 접근자(Getter, Setter)에 의해 결정되며, 필드를 사용하지 않는다.<br>
4. 코틀린은 클래스의 접근자에서 자신의 프로퍼티에 접근하기 위해 'field'키워드를 사용하고, 이것을 'Backing Field'라고 한다.<br>
5. 코틀린의 클래스는 기볹거으로 상속이 닫혀 있고, 상속을 허용하려면 'open'키워드를 사용해야 한다.<br>
6. 코틀린은 클래스를 위임하기 위해 'by' 키워드를 사용할 수 있다.<br>
7. 코틀린은 프로퍼티도 위임이 가능하며, 위임을 하기 위해서는 역시 'by'키워드를 사용한다.<br>
8. 코틀린의 프로퍼티 위임은 Getter, Setter연산자를 구현한 클래스로 위임하거나, 표준 라이브러리에서 제공하는 'lazy, observable, map'등으로 위임할 수 있다.<br>
9. 코틀린은 자주 사용되는 '싱글턴(Singleton)'패턴을 대체하는 'object'클래스를 사용할 수 있다.<br>
10. 코틀린의 'Data'클래스에서는 'toString, equals, hashCode'메소드가 자동으로 구현된다.<br>
11. 코틀린의 클래스는 Java와 가시성이 일부 다르다. 특히 코틀린은 package변경자가 없고, 모듈 가시성인 'internal'을 지원한다.<br>
12. 코틀린은 클래스 내부에 클래스를 선언하는 경우 기본적으로 '중첩클래스'가 된다. Java와 같이 '내부 클래스'로 선언하려면 'inner'키워드를 사용한다. <br>

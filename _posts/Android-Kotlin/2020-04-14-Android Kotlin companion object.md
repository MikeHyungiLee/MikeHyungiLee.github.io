---
layout: post
title:  Kotlin "companion object"
categories: Android-Kotlin
comments: true
---

### <strong>companion object ?</strong><br>

Kotlin은 클래스에 static 필드를 갖게 할 수는 없지만, companion object의 구조를 이용해서 Java의 static 메소드와 동일한 동작을 수행할 수 있다.<br>

    data class Book(val title: String, val price: Int){
        companion object {
            const val FREE_PRICE = 0
            fun newFreeBook(title: String) = Book(title, FREE_PRICE)
        }
    }

    fun main(){
      val book = Book.newFreeBook("Free Kotlin")
      println(book)
    }

위와 같이 companion object 뒤의 {}안에는 일반 클래스의 본체와 같이 구현을 한다. 위와 같이 도우미 개체를 정의하면 Book 클래스 안에 내재 된 싱글 톤 인스턴스(Singleton Instance)가 생성되며, Book.[Field name]형태로 액세스 할 수 있다. <br>

companion object는 <strong><font color="Red">자체가 클래스 정의를 가지고 있으며, 외부에서 정의 된 클래스의 인스턴스가 아니다.</font></strong><br>
Book.xxx()라는 접근방식을 보면, 마치 Book 클래스의 싱글톤 인스턴스가 만들어지고 있는 것처럼 보이지만, Book인스턴스가 만들어지는 것은 아니다.<br>
위의 Book.xxx()라는 문장은 사실 <strong>Book.Companion.xxx()</strong>이 생략 기법이다. 이 점에서 companion object는 Book 클래스의 인스턴스와는 별개임을 알 수 있다.<br>

위와 같이 companion object{}의 형태로 작성할 수 있지만, 이 companion object에 이름을 넣어줄 수도 있다.<br>

    data class Book(val title: String, val price: Int){
        companion object Factory{
          const val FREE_PRICE = 0
          fun freeBook(title: String) = Book(title, FREE_PRICE)
        }
    }


위의 도우미 객체는 Book.Factory.[Field name] 형태로 액세스 할 수 있다.<br>
<strong>companion object는 클래스 내에서 하나 밖에 정의할 수 없다.</strong>


### 전체적인 학습내용을 복습한다.<br>
1.

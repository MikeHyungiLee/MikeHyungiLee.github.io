---
layout: post
title:  Android Kotlin 범위 함수 사용정리
categories: Android-Kotlin
comments: true
---

이번 포스팅에서는 Kotlin 범위 함수 사용에 대해서 정리한다.<br>
<strong>Kotlin의 표준 라이브러리에는 "범위함수"라는 4가지 기능</strong>이 있다.<br>
<strong><font color="Blue">let, with, run, apply</font></strong>이다.<br>

### <strong>.let ?</strong><br>

    val s = "hoge".let{it.toUpperCase()}
    println(s) // HOGE

위의 코드에서 알 수 있듯이 <strong>let은 어떤 형태의 확장 기능</strong>이다.<br>
위의 예에서는 String 인스턴스를 "hoge"를 it으로 받아 처리하고 있다. <br>

다른 예시로, <strong>예를 들어 String? 변수 foo의 대소 표현을 얻고 싶은 경우에는 아래와 같이 작성할 수 있다.</strong><br>

    val upperCase : String? = foo?.let{it.toUpperCase()}

foo가 null인 경우에는 ?. 호출에 의해 let이 실행되지 않고 null을 반환한다.<br>
foo가 null이 아닌경우, let이 실행 it.toUpperCase()에 의해 foo 대문자 표현을 반환한다.<br>    

***

### <strong>with ?</strong><br>

    val s = with("hoge"){this.toUpperCase()}
    println(s) // HOGE

위의 코드에서 알 수 있듯이 <strong>let과 달리 확장함수</strong>가 없다.<br>
첫 번째 인수에 <strong>임의의 형태 T</strong>를 취한다. <br>
this는 "hoge"를 의미하며, 선택적이므로 {toUpperCase()}로 기술해도 된다.<br>

다른 예시로, <strong>예를 들어 String? 변수 foo의 대소 표현을 얻고 싶은 경우에는 아래와 같이 작성할 수 있다.</strong><br>

    val upperCase : String? = foo?.let{it.toUpperCase()}

foo가 null인 경우에는 ?. 호출에 의해 let이 실행되지 않고 null을 반환한다.<br>
foo가 null이 아닌경우, let이 실행 it.toUpperCase()에 의해 foo 대문자 표현을 반환한다.<br>  

***  

### <strong>run ?</strong><br>

    val s = "hoge".run{toUpperCase()}
    println(s) // HOGE

<strong>let 그리고 with이 합쳐진 버전이다.</strong><br>
첫 번째 인수에 <strong>임의의 형태 T</strong>를 취한다. <br>
this는 "hoge"를 의미하며, 선택적이므로 {toUpperCase()}로 기술해도 된다.<br>
인스턴스를 생성하고 각종 설정을 한 후 실제로 바로 사용하기 위해서 사용된다.<br>

***

### <strong>.apply ?</strong><br>

우선 .apply를 사용해서 recyclerView의 LayoutManager와 adapter를 초기해준 아래 예를 같이 살펴보자. <br>

    private fun initRecyclerView(){
        // apply 를 사용해서 layoutManager 와 adapter 를 지정해주었을때,
        recycler_view.apply {
            layoutManager = LinearLayoutManager(this@MainActivity)
            blogAdapter = BlogRecyclerAdapter(context,[dataSet])
            adapter = blogAdapter
        }

        // recycler_view를 지정해주면서 layoutManager 와 adapter 를 지정해주었을때
        recycler_view.layoutManager = LinearLayoutManager(this@MainActivity)
        blogAdapter = BlogRecyclerAdapter(this,[dataSet])
        recycler_view.adapter = blogAdapter
    }

확실히 apply annotation을 사용해서 recycler_view를 초기화 시켜주면, 매번 recycler_view를 호출해서 사용하지 않아도 가볍게 layoutManager와 adapter 키워드만으로도 초기화 시켜줄 수 있다.

### 전체적인 학습내용을 복습한다.<br>
1.

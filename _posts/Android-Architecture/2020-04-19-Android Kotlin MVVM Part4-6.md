---
layout: post
title:  Java MVVM Part4 ~ 6
categories: Android-Architecture
comments: true
---

<strong>#4 Android MVVM Architecture Tutorial - User Login using Retrofit<br></strong>
<strong>#5 Android MVVM Architecture Tutorial - Room Database Setup<br></strong>

<strong>참고</strong>:[https://www.youtube.com/watch?v=67bdklHmXA8&list=PLk7v1Z2rk4hjVaZ8DZKe8iT9RIM9OUrwp&index=1](https://www.youtube.com/watch?v=67bdklHmXA8&list=PLk7v1Z2rk4hjVaZ8DZKe8iT9RIM9OUrwp&index=1)<br>

<strong><font color="Red">Retrofit API에 대해서 더 자세하게 알고 싶다면, </font></strong>
3. Retrofit Android Tutorial - What is REST API ?<br>
[https://www.youtube.com/watch?v=30GSz20AHV4&t=10](https://www.youtube.com/watch?v=30GSz20AHV4&t=10) <br>

13. Retrofit Android Tutorial - Sign Up using Retrofit POST<br>
[https://www.youtube.com/watch?v=xtCmFEaQENc&t=3](https://www.youtube.com/watch?v=xtCmFEaQENc&t=3) <br>

Android Room Tutorial - Building a Basic Notes App<br>

[https://www.youtube.com/watch?v=9iF2qEF28Do&list=PLk7v1Z2rk4hg_ywZffPgRTmJoy2XWs02d](https://www.youtube.com/watch?v=9iF2qEF28Do&list=PLk7v1Z2rk4hg_ywZffPgRTmJoy2XWs02d)<br>

※ 노트정리 (Part4 ~ 5)<br>
<img src="/images/android/2020-04-19/2020-04-19 Room database note.png" alt="blog capture" width="500" title="capture img"><br>

이번 Part4, 5에서는 작성했던 AuthViewModel클래스와 Repository클래스를 연결하는 작업을 해볼 것이다.<br>
폴더 구조는 위에 첨부한 노트필기에서와 같이 data패키지가 있고, 그 아래에 있는 network 패키지(remote data source)와 db 패키지(model - Room database)로 구성되어 있다. <br>

><strong><font color="Blue">Api interface 작성하기</font></strong><br>
>>우선 data 패키지 아래에 network 패키지를 작성하고, MyApi 인터페이스를 작성해준다.<br>
>>이 인터페이스 내부에서는 remote server에서의 email과 password를 User에 의해 입력받은 email과 password과 비교해서 로그인이 성공했는지 실패했는지 확인할 수 있는 userLogin() 메소드가 있다. <br>

><strong><font color="Blue">위에서 작성한 Api 인터페이스를 UserRepository 클래스에 구현해준다.</font></strong><br>
>> 클래스 내부에 userLogin() 메소드를 작성해주고, 이 메소드는  LiveData<String>를 반환해준다.<br>
>> 반환되는 LiveData<String> 값은 MyApi 인터페이스에서 작성해준 userLogin메소드의 callback 함수로부터 반환된 값을 기준으로 한다.<br>

<strong><font color="Red">※ Room database setup</font></strong><br>
다음으로 구성해줄 부분은 <strong>"model"</strong>부분으로, 기존의 data클래스 아래에 <strong>db</strong> 패키지를 작성해주고, 그 아래에 필요한 코드를 구성해준다.<br>

<strong>db패키지의 아래에는</strong> <br>
① Room database를 초기화 시켜주고, Dao의 getter abstract 메소드가 위치한다. - (C)AppDatabase<br>
② Room database로부터 데이터를 insert, select하는 @Dao interface를 작성한다. - (I)UserDao<br>
③ db 클래스 내부에 entities 패키지를 작성해주고, 보내줄 데이터의 entity클래스를 작성한다. - (data C)User<br>

<strong><font color="Red">#6 Android MVVM Architecture Tutorial - Using Coroutines</font></strong><br>
이번에는 위에서 구성한 Room database setting을 통해서 내부 DB에 로그인한 User의 token정보를 저장해볼 것이다.<br>

User의 token정보를 저장하기에 앞서, 우선 <strong><font color="Red">"Simplify Retrofit calls using coroutine" Retrofit의 callback function의 작성을 Kotlin의 Coroutine을 활용해서 간단하게 작성해볼것이다..</font></strong>

<strong>【code refactoring (UserRepository.kt)】</strong><br>

<strong><font color="Blue">기존 코드(Retrofit callback function)</font></strong>

      // 아래와 같이 해주기 보다는 Repository 에서 Api instance 를 초기화 시켜주고 사용하는 것이 좋다.
      // 이 부분은 차후에 수정해보기
      MyApi().userLogin(email, password)
          .enqueue(object: Callback<ResponseBody>{
              override fun onFailure(call: Call<ResponseBody>, t: Throwable) {
                  loginResponse.value = t.message
              }

              override fun onResponse(
                  call: Call<ResponseBody>,
                  response: Response<ResponseBody>
              ) {
                  if(response.isSuccessful){
                      loginResponse.value = response.body()?.string()
                  }else{
                      loginResponse.value = response.errorBody()?.string()
                  }
              }
          })

<strong><font color="Blue">수정된 코드(Kotlin coroutine)</font></strong><br>

    // Api 메소드를 suspend fun 메소드로 수정한 뒤에 Repository method
    suspend fun userLogin(email: String, password: String) : Response<AuthResponse>{
        return MyApi().userLogin(email, password)
    }

<strong>【code refactoring (AuthViewModel.kt)】</strong><br>

<strong><font color="Blue">기존 코드(AuthViewModel.kt)</font></strong><br>
기존에 Retrofit call함수로 코드를 작성했을때는 아래와 같이 작성해주었다.<br>

    val loginResponse = UserRepository().userLogin(email!!, password!!)
    authListener?.onSuccess(loginResponse)

하지만, suspend fun로 메소드를 작성해주면 호출해서 사용하는 곳이 suspend 메소드이거나 Coroutine scope 내부에서 호출해주어야 한다. 따라서 아래와 같이 코드를 작성해주었다.<br>

<strong><font color="Blue">수정된 코드(AuthViewModel.kt)</font></strong><br>

    // util > Coroutines 에 작성해 준 main() 메소드를 사용해서 실행해준다.
    Coroutines.main {
       val response = UserRepository().userLogin(email!!, password!!)
       if(response.isSuccessful){
           authListener?.onSuccess(response.body()?.user!!)
       }else{
           authListener?.onFailure("Error code: ${response.code()}")
       }
    }

기존에 LoginActivity에서 loginResponse의 변화를 observe하는 처리를 해주었는데, ViewModel 클래스에서 CoroutineScope의 main thread에서 처리를 해주었기 때문에, 별도로 Activity에는 Observe처리를 해주지 않아도 된다.<br>

코드를 작성해줄때, 공통적으로 사용되는 메소드는 잘 정리해서 공통화처리해주어야 한다.<br>

    //util/Coroutines.kt (Object class)

    object Coroutines{
      //parameter : coroutine function (suspend function)
      fun main(work: suspend (()->Unit)) =
          CoroutineScope(Dispatchers.Main).launch{
              work()
          }
    }

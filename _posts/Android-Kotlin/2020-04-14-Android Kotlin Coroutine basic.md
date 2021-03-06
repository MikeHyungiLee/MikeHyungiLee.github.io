---
layout: post
title:  Android Kotlin Coroutine Basic
categories: Android-Kotlin
comments: true
---

### <strong>Coroutine ?</strong> <br>

Work with Background thread <br>
Coroutine은 AsyncTask 와 같이 Threading하는 방법 중에 하나이다.<br>

<img src="/images/android/2020-04-16 coroutine thread.png" alt="blog capture" title="capture img">

<strong>※ 아래와 같은 상황에서 Coroutine은 유용하게 쓰인다.</strong><br>
① Request to network retrofit volley 등의 통신 라이브러리를 사용할때, Main Thread가 Block된다.<br>
② Accessing the internal SQLite database on the phone. ex) Room database<br>

<strong><font color="Red">위의 두가지 경우에서 일반적으로 background thread가 사용이 된다.</font></strong><br>

simulate network request and internal room database.<br>

<strong><font color="Blue">Sequence</font></strong><br>
(1) Get the result value from background thread.<br>
(2) Take the result and then display on the main thread.<br>

Android 개발을 하다보면 Network나 내부 데이터베이스로부터 데이터를 취득해서 순차적으로 취득한 데이터를 처리해야 되는 경우가 있다. <br>
이런 경우는 이미 경험을 해봤었기 때문에 얼마나 큰 문제인지 알고 있다. 이 문제를 해결하기 위해서는 RxJava나 callback함수를 사용해서 작성을 하면, 코드가 매우 복잡해지기 때문에, Coroutine을 사용해서 작성을 하면 Simple하게 코드를 작성할 수 있다. <br>

① Gradle에 Coroutine과 관련된 dependencies를 추가한다.<br>

    def coroutines_version = "1.2.1"
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:$coroutines_version"
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-android:$coroutines_version"

② debug용으로 log를 확인하기 위해 "logThread" 메소드를 작성한다.<br>

    private fun logThread(methodName: String){
        println("debug: ${methodName}: ${Thread.currentThread().name}")
    }

③ 테스트용으로 Api로부터 결과값을 가져오는 메소드(suspend)를 두개 작성한다. 이는 순차적으로 취득하는 데이터를 최종적으로 Main thread의 UI요소에 반영하기 위함이다.<br>

    private suspend fun getResult1FromApi():String{
        logThread("getResult1FromApi")
        delay(1000) // sleep single coroutine
        //Thread.sleep(1000) // sleep all coroutine
        return RESULT_1 // "Result #1"
    }

    private suspend fun getResult2FromApi(): String{
        logThread("getResult2FromApi")
        delay(1000)
        return RESULT_2 // "Result #2"
    }

④ 위에서 작성한 Api취득 메소드를 fakeApiResult() 메소드(suspend) 내에서 처리하도록 작성한다. <br>
   여기서 테스트해볼 것은 api로부터 취득한 값을 UI상에 표시하는 테스트를 해볼 것이다. 하지만 <strong>현재 fakeApiResult()메소드가 실행되는 thread는 Main thread가 아닌 Background thread</strong>이므로, <strong><font color="Red">UI에서 처리하기 위해서는 취득한 값을 "Main thread"로 보내서 UI에 표시처리해야 한다.</font></strong><br>

    private suspend fun fakeApiResult(){
        val result1 = getResult1FromApi()
        println("debug: $result1")
        setTextOnMainThread(result1)

        // result1 부분이 처리된 후에 result2부분이 순차적으로 실행될 것이다.
        val result2 = getResult2FromApi()
        setTextOnMainThread(result2)
        //text.setText(result1) //이 작업은 crash 될 것이다.
        // 그 이유는 background thread 에서 작업을 하고 있고,
        // 실제 UI와 interact 하고 있는 thread 는 Main thread 이기 때문이다.
    }

<strong><font color="Blue">setTextOnMainThread() 메소드 (Main thread로 thread를 전환하여 취득한 결과 값을 UI반영하기)</font></strong>

    private suspend fun setTextOnMainThread(input: String){
        //CoroutineScope(Main)로 하거나
        withContext(Main){
          setNewText(input)
        }
    }

<strong><font color="Blue">UI 상에 있는 TextView에 text를 setting하는 메소드</font></strong>

    private fun setNewText(input: String){
        val newText = text.text.toString() + "\n$input"
        text.text = newText
    }

⑤ 마지막으로 onCreate()메소드에 작성한 코드를 살펴보자. 이 코드에서 주목해야 될 부분은 <strong><font color="Red">"CoroutineScope"</font></strong>이다. CoroutineScope의 option으로는 <strong><font color="Blue">IO, Main, Default</font></strong>가 있다. 각 option은 다른 Thread 기능을 하는데, <strong>IO(Input/Output) thread의 경우, Network, local database interaction 기능</strong>을 하며, <strong>Main thread</strong>의 경우, UI 요소와 상호작용하는 역할을 한다. 이외에 Default option은 heavy competition work를 다룰때 사용한다.<br>

    override fun onCreate(savedInstanceState: Bundle?) {
          super.onCreate(savedInstanceState)
          setContentView(R.layout.activity_main)

          button.setOnClickListener{
              // IO(Network, local database interaction),
              // Main(Main thread, interact with UI),
              // Default(heavy competition work)
              CoroutineScope(IO).launch {
                  //launch (coroutine builder)
                  fakeApiResult()
              }
          }
    }    

참고 : [Android coroutines codelab](https://codelabs.developers.google.com/codelabs/kotlin-coroutines/#0)


### 전체적인 학습내용을 복습한다.<br>
1.

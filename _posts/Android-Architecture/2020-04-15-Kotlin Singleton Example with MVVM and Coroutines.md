---
layout: post
title:  Kotlin Singleton Example with MVVM and coroutines
categories: Android-Architecture
comments: true
---

### Kotlin Singleton Example with MVVM and coroutines<br>

이번 Post에 정리할 내용은 아래와 같다.<br>
2 examples :<br>

1) Quick "how to"<br>

2)Practical example<br>
-Retrofit<br>
-Coroutines<br>
-MVVM<br>

Singletons

Instance of an object <br>
reuse the instance <br>
Retrofit instance <br>
Repository instance <br>
User sessions <br>
Dagger(Dependency Injection/Provide Singleton)
Dagger라이브러리는 좀 어렵다. 나중에 별도의 강의로 이해하도록 하자.<br>

<strong><font color="Red">자 이제 실제로 Singleton 패턴의 클래스를 Kotlin으로 작성해보자.</font></strong><br>

① 우선 models패키지를 작성을 하고, 그 안에 User라는 data class를 작성해준다. <br>
② 다음으로 ExampleSingleton을 이름으로 하는 Object클래스를 작성한다. 이 클래스 안에는 앞서 작성한 User클래스를 아래와 같이 객체를 만들어준다.

    val singletonUser: User by lazy {
      User("email@gmail.com", "username", "image.png")
    }

<strong>lazy키워드를 사용해서 변수를 위임하면 실제로 해당 속성이 호출되서 사용될때, 초기화가 된다.<br>
(클래스가 인스턴스화되는 타이밍에는 해당 속성은 메모리상에 초기화되지 않는다) </strong><br>

③ MainActivity의 onCreate 메소드 내에서 Singleton클래스 내부에서 작성한 singletonUser 변수의 hashCode를 확인해서 실제 화면의 configuration(portrait/landscape)가 변경이 되었을때, 같은 메모리 주소를 반환하고 있는지 확인해본다. <br>

    println("DEBUG: ${ExampleSingleton.singletonUser.hashCode()}")

아래와 같이 화면의 configuration을 바꿨을때, 매번 같은 hashCode를 반환함을 알 수 있다.<br>

    D/EGL_emulation: eglMakeCurrent: 0xdb71a480: ver 3 0 (tinfo 0xdb70f7a0)
    I/System.out: DEBUG: -1198862957
    D/EGL_emulation: eglMakeCurrent: 0xdb71a480: ver 3 0 (tinfo 0xdb70f7a0)
    D/EGL_emulation: eglMakeCurrent: 0xdb71a480: ver 3 0 (tinfo 0xdb70f7a0)
    I/System.out: DEBUG: -1198862957
    D/EGL_emulation: eglMakeCurrent: 0xdb71a480: ver 3 0 (tinfo 0xdb70f7a0)

④ 다음으로, api 패키지를 작성하고, MyRetrofitBuilder(Object클래스)와 ApiService 인터페이스를 작성해볼 것이다. <br>
MyRetrofitBuilder클래스를 Object클래스 타입으로 작성하는 이유는 Kotlin에서는 Object클래스로 작성한다는 의미가 바로 'Singleton'으로 작성하겠다는 의미이기 때문이다. ApiService인터페이스에서는 Retrofit을 사용해 통신상으로터 데이터를 취득하는 메소드를 작성할 것이다.<br>
<strong><font color="Blue">MyRetrofitBuilder.kt</font></strong>

    object MyRetrofitBuilder {

        const val BASE_URL = "https://open-api.xyz/"

        // Singleton Retrofit builder
        val retrofitBuilder: Retrofit.Builder by lazy {
          Retrofit.Builder()
          .baseUrl(BASE_URL)
          .addConverterFactory(GsonConverterFactory.create())
          // 서버로부터 호출되는 데이터의 형식은 JSON형태이므로, 이를 Convert할 Converter가 필요하다.
          // Gson Converter = JSON objcet -> Java object
        }

        // Singleton apiService (Network request)
        val apiService: ApiService by lazy {
          retrofitBuilder
          .build()
          .create(ApiService::class.java)
        }

    }

<strong><font color="Blue">ApiService.kt</font></strong>

    interface ApiService {

        @GET("placeholder/user/{userId}")
        // 여기서 사용되는 suspend fun은 'coroutine'을 사용하기 위한 fun이다.
        // use 'coroutine' fun return the date from network.
        suspend fun getUser(
            @Path("userId") userId: String
        ): User
    }

'suspend fun'을 사용하면 'coroutine'을 사용한다는 의미이다. <br>

⑤ <strong>Repository</strong>패키지 추가하고, Repository Object클래스 작성하기.<br>

    object Repository{

        var job: CompletableJob? = null

        fun getUser(userId: String): LiveData<User> {
          // job을 초기화시켜준다.
          job = Job()
          return object: LiveData<User>(){
              override fun onActive(){
                super.onActive()
                // 우선 job이 null인지 아닌지 검사를 한다.
                job?.let{ theJob->
                  // job이 null이 아닌경우, 실행을 한다.
                  // IO(Dispatchers)+theJob으로 유니크한 CoroutineScope를 background thread에 생성을 한다.
                  CoroutineScope(IO+theJob).launch{
                    val user = MyRetrofitBuilder.apiService.getUser(userId)
                    // live data를 background thread에 해줄 수 없으므로,
                    // 우선 MAIN 스레드로 전환을 하고, live data를 setting해주어야 한다.
                    withContext(Main){
                      value = user
                      theJob.complete()
                    }
                  }
                }
              }
          }  
        }
        // job을 calcel하는 method이다.
        fun cancelJob(){
            job?.cancel()
        }
    }

⑥ MainViewModel 클래스를 작성한다.<br>

    class MainViewModel : ViewModel() {
        private val _userId: MutableLiveData<String> = MutableLiveData()

        // Transformations _userId에 변화가 생기면 .switchMap 이 trigger 되고 {}안에 코드가 실행된다.
        val user: LiveData<User> = Transformations
              .switchMap(_userId){
                  // 기존 _userId에 변화가 생겼으니, 업데이트를 해주어야 한다.
                  // 따라서, Repository.getUser를 통해서 새로운 uerId를 취득해서 위에 String변수를 초기화 시켜준다.
                  Repository.getUser(it)
              }

        fun setUserId(userId: String){
             val update = userId

             // 현재의 userId가 이미 setting 되었다면 종료한다.
             if(_userId.value == update){
                  return
              }
             // 기존의 userId를 update된 새로운 userId로 초기화시킨다.
              _userId.value = update
        }  

        // Repository에서 작성한 cancelJobs() 메소드를 viewModel클래스의 cancelJobs()메소드 안에 작성해준다.
        fun cancelJobs(){
            Repository.cancelJobs()
        }    
    }

⑦ MainActivity에서 작성한 MainViewModel클래스의 instance를 작성해서, Observe(변수의 변화가 감지되었을때)를 작성한다.

    class MainActivity : AppCompatActivity() {

        lateinit var viewModel: MainViewModel

        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            setContentView(R.layout.activity_main)

            viewModel = ViewModelProvider(this).get(MainViewModel::class.java)

            viewModel.user.observe(this, Observer {user ->
                println("DBUG: $user")
            })
            viewModel.setUserId("1")
        }

        override fun onDestroy() {
            super.onDestroy()
            viewModel.cancelJobs()
        }
    }
<br>

※ 노트필기 캡쳐 <br>
<img src="/images/android/MVVM Kotlin note.png" alt="blog capture" title="capture img" width="600"><br>

※ 실습했던 Repository : [https://github.com/MikeHyungiLee/MVVMArchitectureKotlin](https://github.com/MikeHyungiLee/MVVMArchitectureKotlin)


### 전체적인 학습내용을 복습한다.<br>
1. <br>

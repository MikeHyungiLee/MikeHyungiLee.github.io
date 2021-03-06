---
layout: post
title:  MVVM architectural design
categories: Android-Architecture
comments: true
---

>MVVM way to structure code  
><strong>MVVM(Model View View-Model)</strong>은 내가 가장 선호하는 architectural design pattern이다.

><strong>Features of MVVM architectural design pattern</strong>
>> 1. UI components are kept away from the business logic  
>> (화면의 각각 UI요소가 비즈니스 로직과 떨어져 있다.)  
>> 2. Business logic is kept away from the database operations  
>> (비즈니스 로직이 데이터베이스를 관리하는 곳으로부터 떨어져있다.)  
>> 3. Easy to understand and read  
>> (이해하기 쉽고 가독성이 높다.)  
>> 4. A lot less to worry when it comes to managing life cycle events   
>> (라이프 사이클 이벤트 관리에 관한 한 크게 걱정할 필요가 없다.)  

><strong>Benefits of using MVVM</strong>  
>> 1. Life cycle state of the app will be maintained  
>> (앱의 라이프 사이클 상태를 유지한다.)  
>> 2. The app will be in the same position the same exact state as when the user left it  
>> (앱은 사용자가 앱으로 부터 나갔을때, 똑같은, 정확한 위치에 위치하게 된다.)  

<strong>Architecture Diagram - outlining an ideal situation when using MVVM</strong>  
<table>
  <tr>
    <td width="50%">
      <img src="/images/android/MVVM architecture diagram.png" alt="blog capture" title="capture img">
    </td>  
    <td width="50%">  
      <b>※ Repository (Data의 Hub와 같은 역할)</b><br>  
      <b>①</b> 우선적으로 살펴볼 부분은 <font color="Red"><b>Remote Data Source부분</b></font>이다. Retrofit API와 같은 통신API를 이용해서 원격지의 데이터를 취득하여 사용한다.<br>
      (Remote data source which is being retrieved by Retrofit library)<br>   
      <br>  
      <b>②</b> 다음으로 살펴볼 부분은 <font color="Red"><b>Model부분</b></font>으로, Room SQLite database를 가지고 있고, 이 부분이 데이터베이스의 Cache된 데이터를 가지게 된다.<br>
      (Room SQLite database which is acting as a database cache)<br>
      <br>
      <b>※ ViewModel (Model for a View)</b><br>
      <b>③</b> 다음으로 살펴볼 곳은 <font color="Red"><b>ViewModel부분</b></font>이다. 이 부분은 Business logic을 가지고 있는 부분이다. 화면에 보여질 데이터를 필터하는 조건처리(if-else)등을 한다. 예를 들어, Custom RecyclerView를 살펴보면, 각각의 리스트 요소에는 이미지와 타이틀 두가지 요소를 가지고 있는데, 이와 같은 View를 위한 Model을 처리하는 부분이라고 생각하면 된다.<br>
    </td>
  </tr>
</table>  
<strong>(Example)Project folder structure</strong>  
(Package)  

① viewmodels :  
><strong>[ViewModel class 작성법]</strong>
<br>    
>① 일반적으로 models의 Object의 이름을 이용해서 [Object name]+ViewModel로 하기도 하지만, <strong>어떤 Activity에서 사용되는 ViewModel인가를 구분하기 위해서 [Activity name]+ViewModel로 class명을 지정하기도 한다.</strong> <br>
>② 해당 ViewModel클래스는　ViewModel클래스를 상속한다.<br>
>③ ViewModel클래스 안에는 MutableLiveData<List<T>> 타입의 변수와 LiveData<List<T>> 두 가지 변수를 선언한다. 이 두 변수 타입의 클래스 구조를 살펴보면  
<strong>MutableLiveData (mutable data / It can be changed - setter method사용 가능)</strong>과 <strong>LiveData (immutable data / It can't be changed - setter method사용 불가능)</strong>가 있다.<br>        
>④ MutableLiveData클래스는 LiveData클래스의 sub class이다. 작성된 코드를 보면, MutableLiveData를 취득하는 Getter함수를 보면, LiveData<List<T>>타입으로 변수를 반환함을 알 수 있다.<br>
> <img src="/images/android/mutableLiveData class ref.png" alt="blog capture" title="capture img" width="300">  <br>
>⑤ MainActivity에서 <strong>작성한 ViewModel클래스를 타입으로 갖는 변수를 선언</strong>하고, onCreate 메소드에서 아래와 같이 초기화를 시켜준다.<br>  
 ex) mMainActivityViewModel = ViewModelProviders.of(this).get(MainActivityViewModel.class);<br>
>⑥ 자 이제 <strong>데이터가 변화하는 것을 관찰하기 위한 설정</strong>을 한다.<br>
(Observe changes done to out viewModel or objects in our view model or in our live data objects) <br>
<img src="/images/android/ViewModel in MainActivity.png" alt="blog capture" title="capture img" width="700">  <br>
>⑦ configuration, 예를들어 screen rotation, lock 화면으로 갔다가 다시 돌아왔을 경우에는 화면의 데이터가 바뀌지 않고, Activity나 Fragment가 바뀌었을때, 변화된 데이터를 화면에 적절하게 표시해주기 위해서, override된 onChanged 메소드에 mAdapter.notifyDataSetChanged();를 작성해준다. 이와 동시에 RecyclerView를 초기화 시켜주는 메소드 안에서도 RecyclerAdapter를 초기화시켜줄때, 아래와 같이 ViewModel class로부터 취득한 데이터로 초기화를 시켜준다. <br>
<strong>mAdapter = new RecyclerAdapter(this, mMainActivityViewModel.getNicePlaces().getValue());</strong>  

② repositories :
><strong>[Repository class 작성법]</strong>   
<br>
>① class의 명명규칙은 [Object name]+Repository로 한다.  
>② 우선 전체적인 클래스 내부는  Singleton으로 작성을 한다.  
>>class의 대표 instance 변수를 private static으로 field variable로 선언을 해준다.
>>데이터를 담을 ArrayList형 dataSet변수를 선언해준다.
>>getInstance() method를 선언해준다. instance가 null일 경우에는 instance를 초기화를 시켜주켜주고 변환해준다.<br>
>>데이터를 가져오기 전에, dataSet변수를 초기화시켜줄 setter method를 선언해준다.<br>
>>해당 Object데이터를 가져오기 위한 MutableLiveData 타입의 getter method를 선언해준다.<br>  
>※위의 내용의 예시가 되는 코드를 아래에 첨부하였다.<br>
<img src="/images/android/2020-04-07 Repository class.png" alt="blog capture" width="500" title="capture img"><br>
<br>

>①＋② ViewModel + Repository : 이제 작성한 Repository를 이용해서 ViewModel의 MutableLiveData를 초기화시켜주는 작업을 할 것이다. <br>
>데이터를 초기화 시켜주기 위해서는 우선 Singleton으로 선언한 Repository의 getInstance를 통해 Repository의 Instance객체를 가져오고, 그 객체를 통해 데이터>>를 가져와서 ViewModel의 mutableLiveData 타입 변수를 초기화시켜준다.<br>
> <img src="/images/android/2020-04-07 initialize ViewModel by using Repo class.png" alt="blog capture" width="500" title="capture img"><br>
<br>

>마지막으로 기존에 LiveData의 변화를 감지하기 위해 Observe한 부분의 이전에 ViewModel에서의 데이터를 초기화시켜주는 작업을 해야한다. (init() method 선언)<br>
> <img src="/images/android/2020-04-07 ViewModel Init method.png" alt="blog capture" width="700" title="capture img"><br>

③ adapters   

④ models   

⑤ 화면에 Progress bar 보여주기

>(실습내용) 화면 우측 하단에 표시되어있는 Floating button을 클릭하면, 새로운 데이터를 추가가 되고, 동시에 약 2초간 Delay가 되면서 Progress bar가 화면의 중앙에 표시가 된다.<br>
<br>
>① ViewModel class에 MutableLiveData<Boolean> 타입으로 field variable를 선언해주고 초기화 시켜준다.<br>
>② addNewValue 메소드를 추가해준다. 앞서 ①에서 만들어 준 변수를 flag변수로 이용해서, true로 setValue를 해주고, 비동기 처리를 위해 AsyncTask class를 이용해서 onPostExecute() 메소드와 doInBackground() 메소드를 Override해서 작성을 해준다. 예시 코드는 아래를 참조한다.<br>
> <img src="/images/android/2020-04-07 Async Progress bar.png" alt="blog capture" width="600" title="capture img"><br>
>③ 이제 MainActivity에서 앞서 선언한 Boolean Live 데이터를 Observe해서 ProgressBar표시를 하도록 설정한다.
> <img src="/images/android/2020-04-07 MainActivity Progress bar .png" alt="blog capture" width="750" title="capture img"> <br>
> <strong>※ 실습을 하게 되면서 알게 된, 공부가 필요하다고 생각되는 부분 : <br></strong>
> ① AsyncTask class는 Deprecated 되었다. 따라서 standard java.util.concurrent 또는 Kotlin concurrency utilities instead를 사용해야 한다.<br>
> ② 이전에 프로젝트를 했을때, Kotlin coroutines 아키텍쳐 컴포넌트를 잘 알지 못했었는데, 비동기 처리를 위한 Class였다. 코틀린을 공부하면서 이 부분도 같이 공부해보자.<br>

  - AsyncTask class ref. : [AsyncTask Ref](https://developer.android.com/reference/android/os/AsyncTask) <br>
  - Kotlin coroutines class ref. : [Kotlin coroutines](https://developer.android.com/topic/libraries/architecture/coroutines) <br>
<br>
※ 직접 내 GitHub에 Repository추가해서 실습하기 <br>
내 GitHub Repository 주소 :  

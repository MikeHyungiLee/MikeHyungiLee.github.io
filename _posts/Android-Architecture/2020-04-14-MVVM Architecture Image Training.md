---
layout: post
title:  MVVM Architecture Image Training
categories: Android-Architecture
comments: true
---

## MVVM Architecture<br>

### Java <br>

<strong><font color="Red">① ViewModel Class</font></strong> <br>

(1) class 선언하기<br>

    public class MainActivityViewModel extends ViewModel {

        private MutableLiveData<List<NicePlace>> mNicePlaces;

        public LiveData<List<NicePlace>> getNicePlaces(){return mNicePlaces;}

    }

클래스를 선언할때에는 ViewModel 클래스를 상속하고, field변수로 MutableLiveData<List<NicePlace>>타입의 변수를 선언해준다. Field변수로 선언을 해줄때는 값이 변화하기 때문에 MutableLiveData 타입으로 선언하지만, 이 값을 읽어올때는 LiveData<List<NicePlace>> 타입으로 선언해준다. <br>

(2) MainActivity에서 작성한 MainActivityViewModel 인스턴스를 만들어서 초기화시켜준다.<br>

    mMainActivityViewModel = ViewModelProviders.of(this).get(MainActivityViewModel.class);

<strong><font color="Red">우선, dependencies에 Lifecycle components dependency를 넣어준다.</font></strong><br>

    // Lifecycle components
    def archLifecycleVersion = '1.1.1'
    implementation "android.arch.lifecycle:extensions:$archLifecycleVersion"
    annotationProcessor "android.arch.lifecycle:compiler:$archLifecycleVersion"

다음으로 해줄 것은 <strong>데이터가 변화하는 것을 관찰하기 위한 설정</strong>을 할 것이다. <br>

    mMainActivityViewModel.getNicePlaces().observe(this, new Observer<List<NicePlace>>() {
        @Override
        public void onChanged(List<NicePlace> nicePlaces) {
            mNicePlaceRecycleAdapter.notifyDataSetChanged();
        }
    });

 이젠 데이터가 변할때마다 변화된 데이터를 화면에 잘 출력할 수 있도록 adapter를 초기화시켜줄때 이 변화된 데이터로 초기화를 시켜준다.<br>

    private void initRecyclerView(){
      mAdapter = new RecyclerAdapter(this, mMainActivityViewModel.getNicePlaces().getValue());
      RecyclerView.LayoutManager linearLayoutManager = new LinearLayoutManager(this);
      mRecyclerView.setLayoutManager(linearLayoutManager);
      mRecyclerView.setAdapter(mAdapter);
    }    

(3) Repository 클래스를 작성해준다.<br>
    이 Repository클래스에서는 실제 화면에 보여지는 Data의 setter와 getter메소드가 있는 클래스이다.<br>
    Repository class는 Singleton으로 작성을 한다.<br>

(4) 작성한 Repository 클래스를 활용하여, ViewModel 클래스에서 init() 메소드를 작성해준다.

    public void init(){
      if(mNicePlaces != null){
          return;
      }
      mRepo = NicePlaceRepository.getInstance();
      mNicePlaces = mRepo.getNicePlaces();
    }

위에 작성한 init() 메소드는 MainActivity에서 ViewModel 클래스를 초기화시켜줄때, 기존의 dataSet변수가 'null'인 경우, ViewModel 클래스 객체를 초기화시켜준 다음에 Repository로부터 데이터를 가져와서 데이터를 초기화시켜주는 작업을 한다.<br>

### Kotlin <br>



### 전체적인 학습내용을 복습한다.<br>
1.

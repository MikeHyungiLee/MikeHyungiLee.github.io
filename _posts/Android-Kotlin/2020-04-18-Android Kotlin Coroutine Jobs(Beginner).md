---
layout: post
title:  Kotlin Coroutine Jobs(Beginner)
categories: Android-Kotlin
comments: true
---

### <strong>Coroutine Jobs in Kotlin ?</strong><br>

<strong>참고</strong>:[https://www.youtube.com/watch?v=UsHTxOILP5g](https://www.youtube.com/watch?v=UsHTxOILP5g)

이번 포스팅에서는 Coroutine Job에 대해서 샘플 어플을 만들어가면서 알아볼 것이다.<br>

인터넷을 통해서 데이터를 취득하는 도중에 속도가 느리거나 timeout, 작업(Job)을 취소해야되는 경우, 과거에는 AsyncTask를 통해서 작업을 조작하는 것은 매우 어렵고 번거로웠다.(현재 deprecated되었다) <br>
이후에 개선되서 나온 것이 "RxJava"이다. 이 RxJava로 기존의 복잡했던 작업들이 좀 더 간단하게 처리할 수 있게 되었다. 각각의 option들이 잘 되어있어서 편리하게 처리할 수 있다는 장점이 있다.(에러가 발생하였을때, 등등..)<br>
그 다음은 "Coroutine"이다. Coroutine은 RxJava보다 더 편리하게 각각의 작업들은 간단하게 컨트롤할 수 있다.<br>

<img src="/images/android/2020-04-18 coroutine job(1).png" alt="blog capture" title="capture img" width="300"><br>

우선 샘플 어플의 처리과정을 정리해보자. <br>
이 어플은 화면에 ProgressBar가 있고, 버튼과 TextView가 있다.<br>
버튼을 눌렀을때 background thread에 해당 task가 실행이 되고, 그 task의 진행상태가 progress bar에 반영이 된다.<br>
(1) task실행이 완료되었을때, TextView에 "Job is complete"표시가 된다.<br>
(2) 실행되는 도중에 "CANCEL JOB #1"을 누르면 "resetting job" Toast 메시지가 표시가 된다.<br>

<strong><font color="Red">※ 내부 처리 작성하기</font></strong><br>

① Field 변수로 Progress bar 관련 변수 <strong>"PROGRESS_MAX=100, PROGRESS_START, JOB_TIME=400(ms)"</strong>와 CompletableJob변수 <strong>"job"</strong>변수를 선언해준다. <br>
② "START JOB #1" 버튼을 클릭했을때, job 변수가 초기화되어 있지 않은 경우 job을 초기화시켜주고, Task 작업을 실행해준다.<br>

<strong><font color="Blue">Coroutine Job의 초기화 메소드</font></strong>

    fun initJob(){
        // button의 text를 setting
        job_button.text = "start Job #1"
        // 초기 TextView의 text를 ""로 초기화
        updateJobCompleteTextView("")
        // job변수의 초기화
        job = Job()
        // job이 취소되거나 완성되었을때 실행되는 invokeOnCompletion 처리하기
        job.invokeOnCompletion{
          it?.message.let{
            var msg = it
            if(msg.isNullOrBlank()){
              msg = "Unknown cancellation error"
            }
            println("${job}was cancelled. Reason: $msg")
            showToast(msg)
          }
        }
        job_progress_bar.max = PROGRESS_MAX
        job_progress_bar.progress = PROGRESS_START
    }

③ job을 초기화할때 사용한 updateJobCompleteTextView(), showToast() 메소드 작성하기<br>

    private fun updateJobCompleteTextView(text: String){
      // GlobalScope를 사용해서 UI요소인 TextView를 업데이트  
      GlobalScope.launch(Main){
        job_complete_text.text = text
      }
    }

    private fun showToast(text: String){
      // GlobalScope를 사용해서 어디서든 Toast 메세지를 보여줄 수 있도록 처리
      GlobalScope.launch(Main){
        Toast.makeText(this@MainActivity, text, Toast.LENGTH_SHORT).show()
      }
    }

④ Job을 reset하는 메소드를 작성하기<br>

    private fun resetJob(){
      if(job.isActive || job.isCompleted){
        job.cancel(CancellationException("Resetting job"))
      }
      // job이 취소된 후에 job이 다시 사용될 수 있도록 job을 초기화시켜준다.
      initJob()
    }

⑤ 확장함수를 사용해서 startJobOrCancel() 메소드를 작성하기<br>

    private fun ProgressBar.startJobOrCancel(job: Job){
      // ProgressBar를 this로 접근할 수 있다.
      if(this.progress > 0){
        // ProgressBar의 값이 0보다 크다면, job을 reset한다.
        resetJob()
      }else{
        job_button.text = "Cancel job #1"
        CoroutineScope(IO+job).launch{
          // job을 background thread(IO+job)에서 실행하기
          // 동시에 progress bar의 상태를 업데이트 해준다.
          for(i in PROGRESS_START .. PROGRESS_MAX){
            delay((JOB_TIME/PROGRESS_MAX).toLong())
            this@startJobOrCancel.progress = i
          }
          // Main thread를 통해 TextView에 "Job is complete"를 업데이트해주기
          updateJobCompleteTextView("Job is complete")
        }
      }
    }

⑥ onCreate() 메소드에 job_button의 setOnClickListener() 이벤트 처리해주기

    job_button.setOnClickListener {
        if(!::job.isInitialized){
            initJob()
        }
        job_progress_bar.startJobOrCancel(job)
    }

### 전체적인 학습내용을 복습한다.<br>
1.

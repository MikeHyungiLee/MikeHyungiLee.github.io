---
layout: post
title: Using Git with Android Studio
comments: true
categories: Git
---

## Android Studio와 Git을 함께 사용 <br>
Android Built-in tool<br>
<br>
① <strong>Android studio에서 새로운 프로젝트를 생성한다.</strong><br>
ex)Project name : AndroidTest<br>

    hyungilee@HYUNGIs-MacBook-Pro ~ % cd ./AndroidStudioProjects
    hyungilee@HYUNGIs-MacBook-Pro AndroidStudioProjects % ls
    AndroidTest	DinnerDecider	Test
    hyungilee@HYUNGIs-MacBook-Pro AndroidStudioProjects % cd ./AndroidTest
    hyungilee@HYUNGIs-MacBook-Pro AndroidTest %
    hyungilee@HYUNGIs-MacBook-Pro AndroidTest % pwd
    /Users/hyungilee/AndroidStudioProjects/AndroidTest
    hyungilee@HYUNGIs-MacBook-Pro AndroidTest % git branch
    fatal: not a git repository (or any of the parent directories): .git

② <strong>$git init</strong>을 Android Studio IDE상에서 해준다.<br>
Android Studio에서 VCS(Version Control System) - Enable Version Control Integration - Git - [OK]  
<br>
③<strong>Git Repository 생성 완료</strong><br>
다시 git branch 명령어를 입력해보면, 아무것도 나타나지 않음을 확인할 수 있다.<br>
Android Studio의 프로젝트 Tree를 보기를 Android에서 Project로 변경.<br>
프로젝트의 하위에 .gitignore파일 내부를 확인.<br>
<strong><font color="Red">(Push할때, 무시하고자하는 항목의 리스트를 .gitignore파일에 추가해준다)</font></strong><br>
.gitignore파일에 추가해야하는 내용에 대해서는 아래의 url에서 확인한다. → [http://gitignore.io/](http://gitignore.io/)<br>
(위의 url에서 AndroidStudio를 검색하면, default로 .gitignore파일에 추가해줄 내용을 확인할 수 있다. 이 내용을 .gitignore파일에 붙여넣어준다)
이제 .gitignore파일의 수정까지 완료된 프로젝트를 GitHub 계정으로 Push해 줄 것이다.  
<br>
④ <strong>GitHub와 프로젝트를 연동하고, 프로젝트의 파일들을 Push한다.</strong>  
Android Studio - VCS - Import into Version Control - Share Project on GitHub  
GitHub 계정을 입력  
Repository name : AndroidTest / Remote name: origin / Description : Testing out Android Git feature - Share   
Everything checked 확인 후 OK  
GitHub계정에서 확인해보면, 프로젝트 전체 파일이 Push 되었음을 확인할 수 있다.  

***

>※ <strong><font color="Red">실습내용</font></strong> : 안드로이드 프로젝트를 생성해서 GitHub와 연동하기  
>① Android Project생성하기. (Project name : <strong>MVVMRecyclerViewJava</strong>)<br>
>② 안드로이드 프로젝트를 생성하고, Repository를 초기화 시켜주고, 추가된 파일을 tracking, commit해준다.

    hyungilee@HYUNGIs-MacBook-Pro AndroidStudioProjects % cd MVVMRecyclerViewJava
    hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava %
    hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava %
    hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava % git init
    Initialized empty Git repository in /Users/hyungilee/AndroidStudioProjects/MVVMRecyclerViewJava/.git/
    hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava % git branch
    hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava % git status
    On branch master

    No commits yet

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
	  .gitignore
	  .idea/
	  app/
	  ......
    nothing added to commit but untracked files present (use "git add" to track)
    hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava % git add .
    hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava % git commit -m "Initial commit"
    [master (root-commit) b9d2268] Initial commit
    37 files changed, 882 insertions(+)
    create mode 100644 .gitignore
    ......

>③ Remote GitHub(Repository)에 해당 프로젝트를 push하도록 한다.
>> (1) 새로운 Repository를 GitHub에서 생성 (Repository name : <strong>MVVMRecyclerViewJava</strong>)<br>
>> (2) Repository의 Http URL을 이용해서 <strong>$git remote add origin [Http URL]</strong>을 해준다.<br>
>> (3) 생성한 프로젝트에 remote GitHub의 repository의 origin이 추가되었으므로, commit된 파일들을 push해준다.<br>

      hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava % git remote add origin https://github.com/MikeHyungiLee/MVVMRecyclerViewJava.git
      hyungilee@HYUNGIs-MacBook-Pro MVVMRecyclerViewJava % git push origin master
      Enumerating objects: 70, done.
      Counting objects: 100% (70/70), done.
      Delta compression using up to 4 threads
      Compressing objects: 100% (53/53), done.
      Writing objects: 100% (70/70), 131.88 KiB | 4.25 MiB/s, done.
      Total 70 (delta 0), reused 0 (delta 0)
      To https://github.com/MikeHyungiLee/MVVMRecyclerViewJava.git
      * [new branch]      master -> master

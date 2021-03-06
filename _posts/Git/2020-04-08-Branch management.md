---
layout: post
title: Branch management
comments: true
categories: Git
---

## Git branch management<br>

(1) <strong>develop branch 작성</strong>

    $ git branch // branch에 있는 전체 branch정보를 확인
    $ git branch develop // develop branch를 작성하기
    $ git checkout develop // develop branch를 checkout하기
    $ git checkout -b develop // develop branch를 작성함과 동시에 새 branch로 switch하기
    $ git push origin develop //remote에 develop 정보를 push하기

***

(2) <strong>feature작성</strong>

    $ git branch //지금 현재 branch가 feature branch인 것을 확인
    $ git branch feature/(feature branch이름) //feature branch를 작성
    $ git checkout feature/(feature branch이름) //feature branch를 checkout
    $ git checkout -b feature/layouts  //branch를 작성함과 동시에 새 branch로 switch하기

(2-1) <strong>feature branch 만들기.</strong><br>
① 새로운 기능 브랜치를 생성하려면 develop 브랜치에서 브랜치합니다.<br>

    $git checkout -b myfeature develop //"myfeature"라는 이름의 브랜치를 만들고 동시에 전환

② 구현이 완료된 기능 분기를 develop에 통합하기.<br>

    $ git checkout develop //develop 브랜치로 전환합니다
    $ git merge --no-ff myfeature //--no-ff 옵션을 지정해두면, 기능 브랜치의 이력이나 Commit 기록을 추가로 남길 수 있습니다.
    Updating ea1b82a..05e9557 (Summary of changes)

③ myfeature 지점은 삭제 해 둡니다

    $ git branch -d myfeature
    Deleted branch myfeature (was 05e9557).

④ GitHub remote repository의 develop branch에 작업한 내용 push하기.

    $ git push origin develop

<strong>#코드를 수정한 후에,</strong><br>  

    $ git add . // 수정된 파일을 tracking list에 추가시켜준다. “.”은 전체 파일을 의미하지만, 각 개별적인 파일을 추가하고 commit해주기 위해서는 구체적인 파일명과 확장자를 입력해주어야 한다.
    $ git commit -m “[commit message]" // 로컬 Repository에 commit하기.
    $ git push origin feature/(feature branch이름)

***

(3) <strong>develop브랜치를 merge시키기</strong>  
     →Merge시키기 전에 merge시키고자 하는 branch의 전 단계 branch로 switch한다.

     $ git checkout develop //feature/(feature branch이름)을 merge시키기 전에 develop branch로 switch한다.
     $ git merge feature/(feature branch이름) // feature branch를 develop branch에 merge시키기
     //merge시킬때, merge option을 사용해서 merge해보기.
     $ git merge --no-ff
     //일반적으로 git merge [branch]하는 것과 git merge --no-ff의 차이점은 아래 첨부한 사진과 같다.

<img src="/images/android/2020-04-08  merge --no-ff.png" alt="blog capture" width="300" title="capture img"><br>

***

(4) 최종적으로 feature branch를 develop branch에 merge했다면, 이 feature branch는 삭제한다.<br>

    $ git branch -d feature/(feature branch명) // feature branch를 삭제

***

(5) 업데이트 된 develop branch를 master branch에 merge시킨다.<br>

    $ git checkout master //master branch에 checkout하기
    $ git merge develop //develop branch를 master branch로 merge하기
    $ git push origin master // feature/(feature branch명)브랜치의 내용을 origin에 upload하기

---
layout: post
title:  Version Control System & Terminal Basic & Git Basic
comments: true
categories: Git
---

## Version Control System : Git <br>
><strong>Version Control ?</strong><br>
<br>
>모든 프로젝트에서 Version Control을 사용해야한다.<br>
>그 이유는 첫번째 혼자 개발을 할때는 큰 버그가 발견되어, 이전 상태로 되돌려야하는 경우 유용하게 사용될 수 있다.<br>  
> <img src="/images/android/2020-04-07 Version Control System(1).png" alt="blog capture" width="300" title="capture img">  
<br>
>두번째 둘 이상의 개발자가 협력해서 같이 프로젝트를 진행하는 경우, 아래의 두 문제에 직면할 수 있다.<br>
><strong>Problem #1 REVERTING BACK TO OLD FILES</strong><br>
><strong>Problem #2 MAINTAING CODE WITHIN A TEAM</strong><br>
><strong><font color="Red"> BACK TO SCENARIO #1</font></strong>둘 이상의 개발자가 협력해서 같이 프로젝트를 진행하는 경우,  
<br>
><img src="/images/android/2020-04-07 Version Control System(2).png" alt="blog capture" width="300" title="capture img"><br>
<br>
> 위의 상황에서 Git은 유용하게 사용될 수 있다.

> <strong>Terminal Basics</strong><br>
> 터미널에서 기본적으로 사용되는 명령어<br>
>><strong><font color="Red">①Terminal Basics - Changing directories</font></strong>  
>><strong>cd [folder] : Change directory</strong>  
>><strong>cd ..  : Move up/back a directory</strong>  
>><strong>cd : Home directory</strong>  
>><strong>ls : Short listing</strong>  
<br>
>><strong><font color="Red">②Terminal Basics - Creating directories & files</font></strong><br>
>><strong>mkdir [dir] : Create new directory  </strong><br>
>><strong>touch  [file] : Create new file ([file]복수 개의 파일을 일괄적으로 생성할 수 있다.)
</strong><br>
<br>
>><strong><font color="Red">③Terminal Basics - copying & renaming files</font></strong><br>
>><strong>mv [file] [dir] : Move file
</strong><br>
>>mv로 단순 파일을 이동시킬때  
>>ex) mv main.js ../  
>>mv 로 파일을 이동할때, 구체적인 파일명을 입력해주면,  rename이 가능하다.  
>>ex) mv main.js ../directory-fun  
>>같은 파일 위치에서 mv명령어를 사용해서 파일명을 재 정의 할 수 있다.  
>>mv awesome.js cats.js (기존의 awesome.js파일의 이름이 cats.js로 변경된다.)  
>><strong>cp [file] [dir] : Copy file to directory</strong>  
<br>
>><strong><font color="Red">④Terminal Basics - deleting files & directories</font></strong><br>
>><strong>rm [file] : Remove a file (연속적으로 여러 파일들을 일괄 삭제할 수 있다.)<br>
>><strong>rmdir [dir] : Remove a directory (내부의 파일들이 전부 삭제되어있어야 한다.)<br>
>><strong>rm -R [dir] : Remove a directory & contents (디렉토리와 내부 파일을 일괄적으로 전부 삭제한다.)<br>

> <strong>Git Basics</strong><br>
> 터미널에서 기본적으로 사용되는 Git명령어<br>
>><strong><font color="Red">①프로젝트 내에서 변경된 파일이나 내용을 확인하는 명령어</font></strong><br>
>><strong>$git status</strong><br>
>><strong><font color="Red">②현재 폴더 위치에 비어있는 Git repository를 초기화시킨다.</font></strong><br>
>><strong>$git init</strong><br>
>><strong><font color="Red">③현재 untracked 상태인 files을 tracking한다.</font></strong><br>
>><strong>$git add [file name + extension]</strong><br>
>><strong>(git status로 확인을 해보면, Changes to be committed로 상태가 변한 것을 확인할 수 있다)</strong><br>
>><strong><font color="Red">④추가한 파일(들)을 message와 함께 Commit한다.</font></strong><br>
>><strong>$git commit -m "[commit message]"</strong><br>
>><strong><font color="Red">⑤다시 이전 버전(상태)로 revert하는 경우,</font></strong><br>
>>우선 <strong>$git log</strong>명령어를 통해 commit된 log기록을 확인한다.<br>
>><strong>$git checkout [commit뒤에 alphanumeric 숫자의 처음 7digit]</strong>
>>→ 이전 Version으로 checkout한 후에는 detached HEAD status로 돌아가기 때문에, <strong>$git checkout -b [new branch name]</strong>를 통해서 새로운 branch로 checkout해주어야 한다.<br>  

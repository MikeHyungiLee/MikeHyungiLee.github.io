---
layout: post
title:  Initial setting
categories: Jekyll
comments: true
---
>① <strong>gem dependencies를 설치</strong>한다.  

    $bundle update  
    $bundle install

>② 아래의 명령어를 실행하여, 로컬로 사이트를 제공한다.

    $bundle exec jekyll serve

>③ <strong><font color="Red">$jekyll serve</font></strong>를 한 뒤에 terminal에 아래와 같은 결과가 나오게 된다면 Server가 제대로 구동된 것이다.

    Configuration file: /Users/hyungilee/MikeHyungiLee.github.io/_config.yml
    Source: /Users/hyungilee/MikeHyungiLee.github.io
    Destination: /Users/hyungilee/MikeHyungiLee.github.io/_site
    Incremental build: disabled. Enable with --incremental
    Generating...
    Skipping: _posts/android/2020-04-07-MVVM architectural design pattern.md has a future date
                done in 0.895 seconds.
    Auto-regeneration: enabled for '/Users/hyungilee/MikeHyungiLee.github.io'
    Server address: http://127.0.0.1:4000
    Server running... press ctrl-c to stop.

>③ <strong>http://localhost:4000</strong> 를 확인해보면, 웹 브라우저 상에서 블로그를 확인해볼 수 있다.  
>Local환경에서 블로그의 수정된 부분을 확인한 뒤에 GitHub에 Push할 수 있어서 편리하다.

<img src="/images/jekyll/2020-04-07-Initial_setting_image(1).png" alt="blog capture" title="capture img">

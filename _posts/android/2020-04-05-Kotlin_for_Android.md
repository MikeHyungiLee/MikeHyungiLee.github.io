---
layout: post
title:  Mongo DB + Android app
date:   2020-04-04 16:43:00
categories: Android
comments: true
---

>><strong>API?</strong> Application Program Interface   
><strong>Get/Post/Put?</strong>  
>기존 데이터베이스를 조작하기 위한 작업으로,API의 문을 두드려서 Request를 보내야 한다.   
>만약 API Request가 매 1, 2초에 하나씩 보낸다면? No! Don't do that!    
><strong>Web Socket?</strong>  
>Web Socket는 위의 매번 1, 2초에 빈번하게 API 요청이 되는 상황을 위한<font color="Red"><strong>"Open door policy free"</strong></font>이다.

><strong>Heroku API</strong> : Built-in Mongo DB로 Mongo DB를 좀 더 편리하게 사용할 수 있도록 해준다.   
><strong>Postman tool</strong> : URL에 직접 데이터를 송수신하는 것을 담당(Body data)  
><strong>Mongo DB</strong> : DB 테이블(Local DB)안에 있는 데이터를 확인  
>>실습내용 : Postman 툴을 이용해서 local DB에 데이터를 전송/등록하고, Robo3T(Robomongo)를 이용하여 local DB에 저장된 데이터를 확인한다.  
>>다음에 공부해보고 싶은 내용 : node.js를 이용하여, 서버쪽을 개발해서 직접 deploy해보기.

***  
① mongo demo 실행하기  

    $mongod

    [initandlisten] exception in initAndListen: NonExistentPath: Data directory /data/db not found., terminating

터미널에서 mongod를 실행했는데, 위와같이 에러가 발생을 한다면, 해당 /data/db의 위치를 찾지 못하고 있는 것이다. 이런 경우에는 Mongo DB의 Path설정을 설정해주면서 실행해주면 된다.  

우선 원하는 Home 위치에서 ./data/db DB를 저장할 폴더를 만들어준다.  

    $mongod --dbpath=/Users/hyungilee/data/db

② API의 소스파일이 있는 폴더로 이동을 해서 로컬에서 호스팅되고 있는 API코드를 mongo DB와 함께 실행시킨다.   

    $npm run dev

③ 다음과 같이 "Database connection ready" 메시지가 나오면 성공적으로 실행이 된 것이고, API에서 처리될 작업 이벤트를 기다리고 있는 것이다.

    > slacky-slack@1.0.0 dev /Users/hyungilee/AndroidStudioProjects/mac-chat-api
    > NODE_ENV=development nodemon -w src --exec "babel-node src --presets es2015,stage-0"

    [nodemon] 1.11.0
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching: /Users/hyungilee/AndroidStudioProjects/mac-chat-api/src/**/*
    [nodemon] starting `babel-node src --presets es2015,stage-0`
    Started on port 3005
    mongodb://localhost:27017/chat-api
    Database connection ready



Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
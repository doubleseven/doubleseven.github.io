---
layout: post
title:  "scala play framework 정리 - 2"
subtitle:   "scala playframework 정리"
description : "scala playframework"
keywords : "scala playframework 란, scala, scala playframework 정리"
categories: dev
tags: scala
comments: true
---

# scala play framework 정리 - 2

## scala play 구조

### app

* controller
	* conf/routes 에서 호출되어 모델과 연결 하여 데이터를 가공 처리 하여 뷰에 던진다
* models
	* 데이터베이스에 연결하여 curd 처리 담당
* views
	* 컨트롤에서 넘어온 데이터를 html에 출력하는 화면을 담당


### conf
* routes
	* 상대주소 url 과 매서드를 매칭해준다 아래 와 같은 방식으로 접근시 / 는 HomeContriller 의 index	메서드로 연결된다.(물론 index 메서드가 구현되어있어야 한다)

	```
	# An example controller showing a sample home page
	GET     /   controllers.HomeController.index
	```

### view
* routes 를 통해 연결된 컨트롤러에서 호출 하며 html 태그를 통해 화면을 만든다
* html 화면에서 @을 사용하여 스칼라 표현을 작성 할 수 있다



## scala play 를 통해 느낀점
..............기존에 php codeigniter 를 사용함으로써 mvc 패턴에 대해서는 그나마 어색한거 없이 적응했지만, controller, view template 에서 scala 문법을 사용하는 부분에서 매우매우 어색하다. 좀 더 공부해서 정리 할 필요가 있다.



#####참고자료

* 누구나 쉽게 스칼라 + 플레이(한빛미디어, 고락윤 저)

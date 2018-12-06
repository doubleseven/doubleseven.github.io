---
layout: post
title:  "scala play framework 정리 - 1"
subtitle:   "scala playframework"
description : "scala playframework"
keywords : "scala playframework 란, scala, scala playframework 정리"
categories: dev
tags: scala
comments: true
---
# scala play framework

진행중인 롤 데이터 분석에 관한 프로젝트에서 scala spark 와 kafka 를 사용한 분석이 끝난 결과를 mysql 에 넣어 php로 출력을 하고 있다.

이부분을 scala 의 웹 프레임워크인 playframework를 사용하여 변경하고자 한다.


## framework?
* 다양한 언어의 framework 가 존재함
	* php
		- **codeigniter**, **laravel**, **yii**, falcon
	* java
		- **spring**
	* python
		- **django**
	* scala
		- Play
* mvc 패턴을 사용한다

### mvc 패턴이란?
```
모델-뷰-컨트롤러(Model–View–Controller, MVC)는 소프트웨어 공학에서 사용되는 소프트웨어 디자인 패턴이다.
이 패턴을 성공적으로 사용하면, 사용자 인터페이스로부터 비즈니스 로직을 분리하여 애플리케이션의 시각적 요소나 그 이면에서 실행되는 비즈니스 로직을 서로 영향 없이 쉽게 고칠 수 있는 애플리케이션을 만들 수 있다.
MVC에서 모델은 애플리케이션의 정보(데이터)를 나타내며, 뷰는 텍스트, 체크박스 항목 등과 같은 사용자 인터페이스 요소를 나타내고, 컨트롤러는 데이터와 비즈니스 로직 사이의 상호동작을 관리한다.
```
* 컨트롤러는 모델에 명령을 보냄으로써 모델의 상태를 변경할 수 있다. (예: 워드 프로세서에서 문서를 편집하는 것) 또, 컨트롤러가 관련된 뷰에 명령을 보냄으로써 모델의 표시 방법을 바꿀 수 있다. (문서를 스크롤하는 것)
* 모델은 모델의 상태에 변화가 있을 때 컨트롤러와 뷰에 이를 통보한다. 이와 같은 통보를 통해서 뷰는 최신의 결과를 보여줄 수 있고, 컨트롤러는 모델의 변화에 따른 적용 가능한 명령을 추가·제거·수정할 수 있다. 어떤 MVC 구현에서는 통보 대신 뷰나 컨트롤러가 직접 모델의 상태를 읽어 오기도 한다.
* 뷰는 사용자가 볼 결과물을 생성하기 위해 모델로부터 정보를 얻어 온다.

## scala play?

* conf/routes 가 중요하다
* actor 모델을 기반으로 한 akka를 사용한다
* 빌드 툴인 sbt(**simple build tool**)를 사용한다


### SBT(Simple Build Tool) 란?
```
SBT는 최신 빌드 도구 중 하나이다. 스칼라로 작성되었고,
스칼라에 사용하기 편한 기능을 많이 제공하기는 하지만, SBT 자체는 범용 빌드 도구이다.
```
* 건전한(?) 의존성 관리
* 의존성 관리에 Ivy를 사용
* 요청이 올때만 업데이트(Only-update-on-request) 모델
* 태스크를 작성할 수 있도록 스칼라 언어 전체를 지원
* 연속으로 명령 실행
* 프로젝트 문맥(환경)하에서 REPL 실행 가능

### Akka란?
```
Akka는 병행(concurrent) 및 분산 처리를 위한 오픈 소스 프로젝트로서 액터(Actor) 모델을 이용하고 있다.
```
* 액터들은 상태를 공유하지 않는다.
* 액터들 간의 통신은 메시지 전달을 통해서 이루어진다. (이벤트 기반 모델)
* 액터간의 통신은 비동기로 이루어진다.
* 각 액터는 전달받은 메시지를 큐에 보관하며, 메시지를 순차적으로 처리한다.
* 액터는 일종의 경량 프로세서다.


## scala play

### 구조
<table>
<tr>
  <th>구조</th><th colspan='2'>설명</th>
</tr>
<tr>
  <td rowspan='4'>app</td><td>controllers</td><td>처리를 담당하는 컨트롤러 모델에서 넘어온 값을 가공하여 뷰로 전달한다</td>
</tr>
<tr>
  <td>views</td><td>html 출력 및 컨트롤러에서 넘어온 데이터 값을 화면에 출력한다</td>
</tr>

<tr>
  <td>models</td><td>데이터베이스와 연결을 하여 데이터를 주고받는 부분을 담당한다</td>
</tr>
<tr>
  <td>기타</td><td>홈페이지가 작동하는 필터 혹은 서비스 같은 추가 비즈니스 로직을 구현한다</td>
</tr>
<tr>
  <td rowspan='2'>conf</td><td>application.conf</td><td>db설정 및 각종 설정을 담당한다</td>
</tr>
<tr>
  <td>routes</td><td>도메인 경로와 컨트롤러를 이어주는 역할을 하는 매우 중요한 녀석</td>
</tr>
<tr>
  <td>test</td><td colspan="2">테스트 코드</td>
</tr>
<tr>
  <td>lib</td><td colspan="2">라이브러리 sbt로 관리하지 않는 라이브러리를 추가하여 관리 할 수 있다</td>
</tr>
<tr>
  <td>logs</td><td colspan="2">로그 파일이 저장되는 폴더</td>
</tr>
<tr>
  <td>public</td><td>CSS,JS</td><td>스타일 이나 자바스크립트를 저장할 폴더</td>
</tr>
<tr>
  <td>project</td><td rowspan='2'>빌드파일(자동)</td><td>빌드하는데 필요한 파일이 정의됨</td>
</tr>
<tr>
  <td>target</td>
  <td>자동빌드 파일이니 수정하지 않도록 주의하자</td>
</tr>
</table>

##### 참고자료
* mvc 패턴 [링크](https://ko.wikipedia.org/wiki/모델-뷰-컨트롤러)
* 누구나 쉽게 스칼라 + 플레이(한빛미디어, 고락윤 저)
* 빌드 도구 SBT(Simple Build Tool)[링크](https://twitter.github.io/scala_school/ko/sbt.html)
* Akka 첫 번째, Akka를 이용한 Concurrent 프로그래밍 시작하기 [링크](http://javacan.tistory.com/entry/akka-1-start)

---
layout: post
title:  "scala sbt setting"
subtitle:   "스칼라 sbt 삽질 설정"
description : "scala sbt"
keywords : "scala sbt, 스칼라 sbt 설정, inteilj scala sbt"
categories: dev
tags: scala
comments: true
---


## scala sbt setting (intillij에서 설정)

지극히 주관적인.. intellij 에서 프로젝트를 구성하는 법에 대해 작성한다

sbt란??
>(simple build tool) 이라 불리며 빌드를 도와주는 범용 툴 이다

sbt를 쓰는 이유?
[sbt참조](https://twitter.github.io/scala_school/ko/sbt.html)
* 건전한(?) 의존성 관리
 * 의존성 관리에 Ivy를 사용
 * 요청이 올때만 업데이트(Only-update-on-request) 모델
* 태스크를 작성할 수 있도록 스칼라 언어 전체를 지원
* 연속으로 명령 실행
* 프로젝트 문맥(환경)하에서 REPL 실행 가능



**inteilj** 에서 scala plug in 을 설치하면 sbt, play(web용framework), idea 로 선택해서 프로젝트를 만들 수 있다

프로젝트를 만들면 아래의 구조를 가진다

* project – 프로젝트 정의 파일들
 * project/build/.scala – 주 프로젝트 정의 파일
 * project/build.properties – 프로젝트, sbt, 스칼라 버전 정의
* src/main – 앱 코드가 이 디렉터리 아래 들어감. 언어에 따라 main 아래 하위 디렉터리를 만들고 그 안에 코드를 넣자. (예: src/main/scala, src/main/java)
* src/main/resources – jar에 추가하고픈 정적 파일들(예: 로그 설정 파일 등)
* src/test – 앱 코드는 src/main에, 테스트 코드는 여기에 넣는다
* lib_managed – 프로젝트에서 사용하는(의존하는) jar 파일들. sbt update를 하면 여기에 jar들이 다운로드됨.
* target – 빌드시 만들어지는 것들이 들어가는 곳(예: generated thrift code, class files, jars)


프로젝트가 잘 생성되면 **build.sbt** 를 수정한다
[sbt setting 참조](https://www.scala-sbt.org/1.0/docs/Basic-Def-Examples.html)

```
lazy val root = (project in file(".")).
  settings(
    inThisBuild(List(
      organization := "com.example",
      scalaVersion := "설치한 스칼라 버전",
      version      := "0.1.0-SNAPSHOT"
    )),
    name := "프로젝트 명",
    libraryDependencies ++= List(
    	lib 및 dependencies를 추가한다. 아래는 스파크 스트리밍을 사용하기 위해 추가함
      "org.apache.spark" % "spark-core_2.11" % "2.2.0",
      "org.apache.spark" % "spark-streaming_2.11" % "2.2.0"
    ),
    retrieveManaged := true
  )
```

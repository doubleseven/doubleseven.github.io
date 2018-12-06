---
layout: post
title:  "180726 프로젝트 회의"
subtitle:   "패스트캠퍼스 데이터 엔지니어링 수업 에서 그룹 프로젝트"
description : "team project"
keywords : "spark, bigdata project, lol api"
categories: data
tags: project
comments: true
---

## 18.07.26 프로젝트 회의

팀명이 정해졌다..

**방구석야스오**

사용할 기술에 대한 회의 및 lol api 분석을 시작했다

<img src="https://bluehyun.github.io/assets/lol/stack.jpg">

## kafka
Apache Kafka(아파치 카프카)는 LinkedIn에서 개발된 분산 메시징 시스템으로써 2011년에 오픈소스로 공개되었다. 대용량의 실시간 로그처리에 특화된 아키텍처 설계를 통하여 기존 메시징 시스템보다 우수한 TPS를 보여주고 있다.

Kafka는 발행-구독(publish-subscribe) 모델을 기반으로 동작하며 크게 producer, consumer, broker로 구성된다.



kafka 를 사용하는 이유는 ..........
> 뭘까?


## apache flume

data 수집기

hadoop 에 붙이기 용이함

kafka 와 유사하여 요즘은 klume( kafka + flume )으로 사용한다.

사용하는 이유는..........................
> 뭘까?


## aws (s3)

아마존!!!!

이유가 있습니까? 아마존인데


## hdfs(aws_ec2 or local)


## apache spark(zeppelin)

이걸 왜 쓰냐고 묻는 바보같은 놈은 없겠지

## rdb
사용자의 분석된 데이터는 rdb 에 넣기로 했다.
등록되어 있지 않은 사용자라면 lol api 를 통해 분석을 하고
기 등록된 사용자라면 기존 데이터를 가져와서 뿌려주고 최신 데이터가 아니면 이때 갱신요청을 받는다

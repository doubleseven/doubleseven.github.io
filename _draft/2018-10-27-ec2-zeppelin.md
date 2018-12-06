---
layout: post
title:  "aws ec2 zeppelin 설치"
subtitle:   "aws ec2 zeppelin 설치"
description : "aws ec2 zeppelin 설치"
keywords : "aws, ec2, zeppelin 설치 aws ec2 zeppelin 설치"
categories: data
tags: zeppelin
comments: true
---
# ec2 zeppelin notebook 설치



## 프리티어는 제플린 안된다!!!!!!!!!!!

ec2 에서 인스턴스를 만든다.

> 프리티어 우분투로 만들었음...프리티어로는 제플린 안된다..하지말자

>java.lang.RuntimeException: OpenJDK 64-Bit Server VM warning: ignoring option MaxPermSize=512m; support was removed in 8.0 OpenJDK 64-Bit Server VM warning: INFO: os::commit_memory(0x00000000d5550000, 715849728, 0) failed; error='Cannot allocate memory' (errno=12) #

> 보안 그룹은 당장은 내ip로만 만들었음

java 설치
openjdk 가 설치가 안된다.


찾아보니
repository 재설정
sudo add-apt-repository ppa:openjdk-r/ppa
update
sudo apt-get update

install
sudo apt-get install openjdk-8-jdk

> 설치된 java 목록 확인 다른게 있으면 아래의 설정으로 변경

sudo update-alternatives -l


sudo update-alternatives --config java
sudo update-alternatives --config javac

# scala install
wget www.scala-lang.org/files/archive/scala-2.11.7.deb
sudo dpkg -i scala-2.11.7.deb



# Spark
wget http://d3kbcqa49mib13.cloudfront.net/spark-1.6.0-bin-hadoop2.4.tgz
tar -xf spark-1.6.0-bin-hadoop2.4.tgz
mv spark-1.6.0-bin-hadoop2.4 ~/spark

# for ec2 set hostname and hosts file
echo $(cat /etc/hostname) | sudo tee -a /etc/hosts

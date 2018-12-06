---
layout: post
title:  "spark(scala) 코딩 가이드"
subtitle:   "spark(scala) 코딩 가이드"
description : "spark coding guide"
keywords : "spark, spark coding guide, scala, 스파크 코딩 가이드"
categories: dev
tags: scala
comments: true
---

# spark 코딩 스타일

## scala 와 약간 다름
**아래에 써놨지만 거의 복붙 수준이다. 너무 잘 정리 되어 있지만 정리 수준으로 작성해본다**

> Java 와 Scala 의 표준 명명 규칙을 따른다

## 명명규칙
* Class, trait, 객체는 카멜을 따라야 함

```
class ClusterManager
trait Expression
```

* Package 는 java 규칙을 따름(소문자)

```
package com.databricks.resoucemanager
```

* 메소드/함수는 카멜을 사용함
* 모든 상수는 대문자로 표기 하고, 연관된 객체에 배치함

```
object Configuration {
	val DEFAULT_PORT = 10000
}
```


* Enum 은 파스칼표기법을 따른다
* Annotation 또한 파스칼표기법 을 따른다.<br>
**scala 공식 가이드와 다르다**

```
final class MyAnnotation extends StaticAnnotaion
```

## 변수 명명 규칙

* 변수는 파스칼표기를 한다
* 변수의 의미가 설명 될 수 있는 이름을 쓴다

```
val serverPort = 1000
val clientPort = 2000
```

## 라인길이
* **라인 길이는 100자를 넘지 않는다**

## 공백 및 들여쓰기
* 연산자 및 할당 연산자 앞 뒤에는 1칸 공백을 두도록 한다

```
def add(int1: Int, int2: Int): Int =  int1 + int2
```

* 콜론 뒤에는 1칸 공백을 둔다

```
// 예시
def getConf(key: String, defaultValue: String): String = {
	//code
}
// 콜론 앞에 공백을 두지 않는다.
def calculateHeaderPortionInBytes(count: Int) : Int = {
	//code
}
// 콜론 뒤에는 공백을 생략하지 않음.
def multiply(int1:Int, int2:Int): Int = int1 * int2
// 이거 여야 하지 않나??
def multiply(int1: Int, int2: Int): Int = int1 * int2
```

* 2칸 들여쓰기(...난 4칸 쓰는데..)

```
if(true)  {
  println("wow")
}
```

## 빈줄
* 아래의 경우에 사용함
	* 연속되는 변수 , 생성자, 함수 또는 내부 클래스 사이에 삽입
	* 한개 또는 두개의 빈 줄을 사용하여 class 혹은 object 선언을 분리함.

## 괄호
* I/O 접근이나 상태 변형에 대한 접근을 가지고 있거나 side-effect를 줄 수 있는 함수는 괄호와 함께 선언한다

```
class Job{
	// blah blah~
	def killJob: Unit

	// blah blah~
	def killJob(): Unit
}
```
* 함수 호출은 반드시 함수 정의를 해줘야함. 함수가 괄호 없이 선언되었으면 괄호 없이 호출되어야 함.
* **문법적인 문제 뿐만 아니라 apply 를 호출 할 때에도 문제가 될 수 있음**

```
class Foo {
	def apply(args: String*): Int
}

class Bar {
	def foo: Foo
}

new Bar().foo // this returns a Foo
new Bar().foo() // this returns an Int
```


## Imports
* **와일드 카드를 이용한 import는 피하도록 한다**
* 6개 이상 패키지에서 import 하는 경우 혹은 implicit 함수를 import 하는 경우는 허용
* 와일드 카드 import 는 외부(import된 패키지)의 변화에 약할 수 있다
* import 를 할 때는 상대 경로가 아닌 절대 경로를 사용함. 상대경로 util.Random 이 아닌 scala.util.Random 을 사용함
* 또한 import 는 순서를 정렬해야한다.
	* java.* 와 javax.*
	* scala.*
	* third-party 라이브러리 (org.*, com.*, etc)
	* 프로젝트 패키지(com.databricks.* 혹은 org.apache.spark)
* 각 그룹안에서 import는 알파벳 순서로 정렬
* IntelliJ의 import 최적화 기능을 사용하여 자동으로 할 수 있다.


```
java
javax
_______ blank line _______
scala
_______ blank line _______
all other imports
_______ blank line _______
com.databricks  // or org.apache.spark if you are working on Spark
```

## 패턴매칭
* 함수 전체가 패턴 매칭을 하는 함수 라면 match 를 함수의 정의로써 같은 줄에 놓음
```
def test(msg: Message): Unit = msg match {
	case ...
}
```
* 함수를 호출 할 때, 아래와 같은 중괄호 안에 (혹은 partial function 안에) 한 개의 case 만 있다면, 같은 줄에 넣어 호출함

```
list.zipWithIndex.map { case (elem, i) =>
	// ...
}
```
만약 여러 개의 ```case``` 문이 존재한다면 아래와 같이 들여쓰기를 한다.
```
list.map {
	case a: Foo => ...
	case b: Bar => ...
}
```

## 익명함수
* 익명 함수를 위한 **여분의 소괄호 및 중괄호를 피함**

```
// 바른 예
list.map { item =>
	...
}

// 바른 예
list.map(item => ...)

//틀린 예
list.map(item => {
	...
})

//틀린 예
list.map { item => {
	...
}}

//틀린 예
list.map({ item => ...})


* 참조
[Databricks Scala Guide](https://github.com/databricks/scala-style-guide/blob/master/README-KO.md?fbclid=IwAR0Rt4iSv7afV98dLo3gF3FqfoI_oG0L_relDbN5lugx3LBMN7jhezFytHQ)

---
layout: post
title:  "패스트캠퍼스 DevOps BOOTCAMP 3기 1주차"
subtitle:   "DevOps 공부"
description : "DevOps, devops, 패스트캠퍼스, 패스트캠퍼스 BOOTCAMP"
keywords : "devops, DevOps,"
categories: books
img: kong.jpg
comments: true
---
# DevOps 구축 BOOTCAMP - 1주차

__애플워치4 사고싶다__

##DevOps

> 데브옵스는 애플리케이션과 서비스를 빠른 속도로 제공할 수 있도록 조직의 역량을 향상시키는 문화 철학, 방식 및 도구의 조합

* 개발(dev) + 운영(ops) 가 합쳐진 말 **일이 많다**
* 계속 변화하고 있음.
* 과거 시점에는 맞는 방법이겠지만 현재 기술 발전 속도로는 따라가지 않는다.
* 개발조직의 **문화** 가 녹아있는 방식 이기에 정확한 정의를 내릴수 있다고 보진 않는다.
* **비즈니스의 발전에 빠르게 대응하기 위한 일렬의 대응**
* 개발자들의 생산성을 높이는데 일조 하며...(반복된 노가다를 자동화 시키는것도 중요하다고 본다)




> # CI / CD 에 대한 개념이해
>
## CI(Continuous Integration) 란?
Build , Test를 실시하는 프로세스를 말하며 이러한 통합 프로세스를 상시로 실시해 주는것을 CI라고 합니다.
>
## CD(Continuous Delivery or Continuous Deploy) 란?
짧은 주기로 소프트웨어를 개발하는 소프트웨어 공학적 접근의 하나로, 소프트웨어가 언제든지 신뢰 가능한 수준으로 출시될 수 있도록 보증하기 위한 것이다. 소프트웨어를 더 빠르게, 더 주기적으로 빌드하고 테스트하고 출시하는 것을 목표로 한다. 이러한 접근은 더 많은 증분 업데이트를 업무 애플리케이션에 적용할 수 있게 함으로써 변경사항의 배포에 대한 비용, 시간, 위험을 줄일 수 있게 한다.
>
참조 [우아한형제들 라이더스 개발팀 모바일에서 CI/CD 도입](http://woowabros.github.io/experience/2018/06/26/bros-cicd.html)




## AWS

### EC2
* Amazon Elastic Compute Cloud(EC2) c가 2개라 ec2
* AWS 에서 제공하는 가상 서버

>
* ami(Amazon Machine Image) amazon linux image 를 뜻함
* MY AMIs 를 통해 설정된 machine image를 만들수있다.
* 서버를 n대 운영함으로써, 외부에서는 정상적인 서비스로 보여지게끔 한다
* 머신 사양에 따른 요금체계가 존재하므로, 어떤걸 사용할지 고민 해야한다
* 클라우드 서비스가 인프라 엔지니어 인건비보다 비쌀경우 인프라 엔지니어를 고용하여 시스템을 구축하는게 낫다

* 네트워크 환경 구성은 aws 물리머신 에서 구분점

* ec2 보안그룹 구성
	* 서버는 안정적으로 유지되야 하고 익명의 사용자가 접근해서는 안된다.
	* 해당 서버의 요청에 대해 허용 , 비허용 목록을 작성한다


> Linux 별 차이
>
> 목적에 맞는 Linux 를 사용하자.
> Cent os, Amazon Linux, Ubuntu, Debian, ETC...
> Amazon Linux를 사용하는 이유는 **docker + container** 를 지원하는 이상적인 운영체제로 커스터마이징 함.

### Amazon linux 2
와
amazon-linux-extras list 라는 명령어를 통해서

nginx1.12

php7.2

lamp-mariadb10.2-php7.2

docker=latest

와!!!!!
다 깔려있다!!!!


amazon-linux-extras 는
해당 서비스의 대해서 버전관리를 보수적으로 한다.

기존 리눅스에선 apt-get, yum 을 통해 버전관리를 했다면
amazon-linux-extras는 관련 문서를 보고 사용가능 한 버전을 사용하여야 한다.

### Virtual Machine

물리 머신 위에 독립적 OS 실행이 가능한 논리적인 가상 OS를 생성하여 실행

- 하나의 서버에서 여러 os를 실행함
- 자원 (cpu, memory)를 공유함

특정 시점에 autoscaling group 를 통해 유동적으로 서버를 늘렸다 줄였다 가능한게
ec2 에서 가상머신으로 구축되어 있기 때문이다


### NginX 설치, 실행
ec2 server 에 접속

sudo ssh -i {pem 키 파일이 있는 위치} ec2-user@{앞서 복사한 DNS 주소} ↵
> __ssh(Secure shell)__
>
> 다른 컴퓨터에 접속하거나 원격 시스템에서 명령을 실행할 수 있는 클라이언트/프로토콜을 의미
> 22번 포트 사용
> -i 옵션으로 비밀번호가 아닌 SSH key로 접속
>
> SSH key는 서버에 저장된 Public Key 와 사용자의 Private Key를 비교하여 확인될때만 접속을 허용
>


sudo su ↵

amazon-linux-extras install nginx1.12 ↵

nginx ↵

1. sudo su 명령어로 root 권한으로 변경
2. nginx1.12 설치
3. nginx 실행
4. 앞서 복사한 DNS 주소로 웹 브라우저에서 접속(NginX 실행 확인)

> web server
>
> http transaction 을 받고 정적인 파일을 요청한 대상에게 보내준다.(html, image file ..)

<br>

> was(Web Application Server)
>
> 동적으로 데이터를 생성하여 응답하는 서버
>
> application(code) logic을 직접 실행하는 서버

### DNS
Domain Name Service

### Port
* TCP/IP 로 접속시 마지막 종단점
* 일반적으로 SSH(22) , HTTP(80) WAS(8080) 을 부여
* 도메인(URL) 로 접속 시 기본적으로 80번 포트를 사용(__생략가능__)
* 보안 강화 목적으로 다른 포트로 변경하기도 한다(__설정과정이 귀찮고, 복잡하기도 하지만, 무작위 접속을 어느정도 예방 가능__)


### Docker

* 컨데이너 기반의 오픈소스 가상화 플랫폼
* 다양한 프로그램, 실행환경을 __컨테이너__ 로 추상화 하고 동일한 인터페이스를 제공하여 프로그램 배포 및 관리를 단순화 할 수 있음
* OS(Host)위에 또 다른 OS(Guest)를 올려야 하는 비효율적인 가상 머신의 단점을 극복하기 위해
나온 가상화 어플리케이션


#### Docker Container
* Docker Engine 위에서 동작하는 가상화 된 OS 어플리케이션
* VM처럼 하드웨어 가상화가 아닌 OS만을 가상화하여 Host OS와 커널 등 겹치는 기능을 공유
* 컨테이너 내에서 동작할 application에 필요한 binary만 패키징되어 가볍고 속도가 빠름




amazon-linux-extras install docker ↵
service docker start ↵
docker pull nginx:latest ↵

1. amazon-linux-extras 레포지토리를 활용해 docker 설치
2. docker 데몬 실행
3. dockerhub에서 nginx 이미지 다운로드

docker images ↵
시 생성된 이미지가 나온다

<img src="bluehyun.github.io/assets/img/docker/week1/docker-image.png">


docker run -d -p 80:80 --name NginX nginx:latest
실행시 에러남 80 포트가 잡혀있기 때문이다

<img src="bluehyun.github.io/assets/img/docker/week1/docker-run-error.png">


docker run -d -p 8080:80 --name NginX nginx:latest ↵ docker ps -a ↵

nginx:latest 이미지를 기반으로 docker container 실행

docker ps -a

실행중인 docker 컨테이너 프로세스 확인


## sub session

#### 간단한 리눅스 명령어들

### ls

* ls -al 의 관한 옵션

### man
man <command> help 보다 자세한 메뉴얼 설명이다


### cd
폴더 이동

### mkdir
폴더 생성

* mkdir -p my-dir/1/2
하면 my-dir/1/2 를 상위폴더 부터 하위 폴더 까지 다 만들어준다

(tree 는 yum , adp 로 설치하여야 함)
tree .   

해당 위치의 트리 구조를 보여준다

### rmdir
폴더 삭제

* rmdir -p my_dir/1/2 하위 폴더 까지 지워줌


### cp
파일 복사

* cp -r origin-dir new-dir origin-dir 의 하위 폴더까지 new-dir 로 복사

### mv
파일 복사


### rm
파일 삭제

* rmdir 폴더만 삭제
* rm 폴더 또는 파일 삭제

### ln
파일링크 바로가기를 만든다라고 보면 된다

### useradd
사용자 등록

adduser ?  useradd ?

amazon linux 2 에서는 adduser 가 useradd로 symbolic link 걸려있음

### userdel
사용자 삭제

userdel -r username 해당 user의 home dircetory 까지 삭제함


### gpasswd

### su, sudo
su

* 목적 사용자의 비밀번호 사용
sudo

* 현재 사용자의 비밀번호와 sudoer 설정 필요


sudo su 에서 sudo su - 를 사용하지 않으면 env(환경변수)변경 되지 않는다.

**man su 를 보면 알겠지만 다른 유저로 변경 시 에는 --login 옵션의 축약인 - 를 사용하여 변경하여라**

### chwon
파일 사용자의 소유권한을 변경한다

-R 폴더의 하위까지 권한 변경함

### chmod
파일 사용권한을 변경한다


### grep
패턴에 맞는 문구를 출력한다
시스템 활성화 되어있는 목록을 출력한다거나 로그 파일에서 패턴으로 검색가능

### head , tail
head 첫부분 부터 출력
tail 뒤에서 부터 출력


### find
파일 검색

find . -name "*test"
현재 디렉토리 하위에 이름이 test 로 끝나는 모든 객체 찾기

find . -iname "*.log" -mtime + 14 -print -exec gzip {} \;

- 마지막 수정일로 부터 14일 경과한  \*.log 파일을 gzip으로 압축

### df , du
df

디스크의 남은 용량

du

디스크의 사용가능 용량

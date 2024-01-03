# Day21

# Docker & Container

**아래 책으로 이론 및 실습 진행**

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5bc753df-e96c-439b-ae97-db169366ffb9)


## 도커

### 도커란?
- 리눅스의 응용 프로그램을 프로세스 격리 기술들을 사용해 컨테이너로 실행하고 관리하는 오픈 소스 프로젝트이다.

https://www.redhat.com/ko/topics/containers/what-is-docker

### 도커엔진
- 컨테이너를 생성하고 관리하는 주체로서 이 자체로도 컨테이너를 제어할 수 있고 다양한 기능을 제공하는 도커의 핵심 프로젝트이디ㅏ.

### Virtual Machine(가상머신) vs Docker Container(도커 컨테이너)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/99876706-c19b-41db-a6f0-ffbd719884d1)

### docker repository설치

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

```bash

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

### docker 명령어

`docker container run diamol/ch02-hello-diamol`로 컨테이너 실행

`docker ps -a`로 컨테이너 상태 확인

`docker rm [Container ID]`로 컨테이너 삭제

`docker container top httpd` 해당 컨테이너 에서 동작중인 프로세스 확인

`docker container logs httpd` 컨테이너 로그 확인

`docker container inspect httpd` 이미지 or 컨테이너 세부정보 출력


### 컨테이너에서 웹 사이트 호스팅

1. `docker run -d -p 8082:80 diamol/ch02-hello-diamol-web`
- 호스트 포트번호 : 컨테이너 포트번호
- -d : 컨테이너를 백그라운드에서 실행하며 커테이너 ID를 출력
- -p : 컨테이너의 포트를 호스트 컴퓨터에 공개

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/50914eb7-4196-451a-ac9b-8b101f9f92bf)


2. 해당 ip와 포트로 접근

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/8dd23ad5-f7e5-491b-bdbd-af9576349d85)


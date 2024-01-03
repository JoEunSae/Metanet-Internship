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

`docker container run diamol/ch02-hello-diamol` : 컨테이너 실행

`docker ps -a` : 컨테이너 상태 확인

`docker rm [Container ID]` : 컨테이너 삭제

`docker container top httpd` : 해당 컨테이너 에서 동작중인 프로세스 확인

`docker container logs httpd` : 컨테이너 로그 확인

`docker container inspect httpd` : 이미지 or 컨테이너 세부정보 출력

`docker stop $(docker container ls --all --quiet)` : 모든 컨테이너 중지

`docker rm $(docker container ls --all --quiet)` : 모든 컨테이너 삭제



### 컨테이너에서 웹 사이트 호스팅

1. `docker run -d -p 8082:80 diamol/ch02-hello-diamol-web`
- 호스트 포트번호 : 컨테이너 포트번호
- -d : 컨테이너를 백그라운드에서 실행하며 커테이너 ID를 출력
- -p : 컨테이너의 포트를 호스트 컴퓨터에 공개

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/50914eb7-4196-451a-ac9b-8b101f9f92bf)


2. 해당 ip와 포트로 접근

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/8dd23ad5-f7e5-491b-bdbd-af9576349d85)

#### 연습문제 : 컨테이너 파일 시스템 다루기

1. index.html생성

2. `docker run -d -p 8080:80 diamol/ch02-hello-diamol-web`으로 컨테이너 실행

3. `docker cp index.html flamboyant_shirley:/usr/local/apache2/htdocs`으로 index.html복사

4. `docker restart flamboyant_shirley`로 컨테이너 재시작

5. 호스트 ip와 포트로 접근

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2f05ec60-0d06-4169-92c5-f2ae200f8a33)

### Dovkerfile(python이미지)

1. 작업할 폴더 생성 mkdir image

2. 해당 폴더에 다운받은 app.py파일 위치

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/7901bb36-41c5-432b-8f6e-ff46c19914a3)


4. Dockerfile생성 `vi Dockerfile`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/d8452a66-6fd1-4af9-b232-227e5d09b3f6)

4. `docker build -t mypython`로 이미지 파일 빌드

5. `docker run -d -p 8085:8080 --name mypython mypython` 빌드한 이미지 컨테이너 실행

6. 해당 ip로 접근

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/14a1f45b-1fce-478f-aa26-8d242486e204)

#### MySQL 컨테이너

1. 같은 네트워크에 서 db에 접근하기 위해 네트워크 생성 `docker network create mynet`

2. 환경 변수만 추가한 Dockerfile생성 

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9e3fc626-8f10-45e4-8519-330634f2c6cc)

3. 이미지 파일 build `docker build -t gooddb .`

4. 컨테이너 실행 docker run -d --network mynet --name gooddb gooddb`

5. Docker파일에 선언한 사용자로 mysql접근 `docker run -it --network mynet --rm mysql mysql -h mysql_server -u root -p`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/343b92b8-60ec-4c68-86ca-8b7a3c0de95d)

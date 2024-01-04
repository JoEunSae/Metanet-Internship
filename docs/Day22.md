# Day22

## 도커 허브 등 레지스트리에 이미지 공유하기

### 도커 허브에 직접 빌드한 이미지 푸시하기

1. `docker login`으로 도커 허브에 로그인

2. `docker tag myhttpd1 goodbird0/myhttpd:1.0` 기존의 Docker 이미지명을 새로운 이름으로 변경하거나, 새로운 태그명을 붙일 때

3. `docker push goodbird0/myhttpd:1.0` 도커 Hub에 이미지 푸시하기

4. `docker pull khalinux/myhttpd:1.0` 도커 허브에 있는 이미지 Pull하기

### 도커 레지스트리 운영

1. Docker Hub의 registry 이미지로 컨테이너 실행 `docker run -d -p 5000:5000 --restart always --name registry registry:2`

2. `sudo vi /daemon.json`파일 생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/daae7258-4c8c-49b4-8c59-9dcec4f39c97)

3. `docker tag myhttpd1 myregistry.local:5000/web/myhttpd:v1.0` 새로 만든 레지스트리 도메인 네임 추가

4. `docker push myregistry.local:5000/web/myhttpd:v1.0` 레지스터리에 이미지 push

5. `docker pull myregistry.local:5000/web/myhttpd:v1.0` 레지스터리에 이미지 pull


## 도커 볼륨을 이용한 퍼시스턴트 스트리지

### 도커 볼륨을 사용하는 컨테이너 실행하기

1. `docker volume create myvol` 볼륨생성

2. 생성한 볼륨을 지정하여 mysql 컨테이너 생성
`docker run -d --network mynet -v myvol:/var/lib/mysql --name mysql_server -e MYSQL_ROOT_PASSWORD=1 -e MYSQL_USER=goodbird -e MYSQL_PASSWORD=1 mysql`

3. mysql에 접속하여 데이터베이스 생성하고 테이블도 생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2ad6909c-6140-42e6-ae51-d1a0412c72e7)


4. 빠져와서 Container를 삭제한다.

5. 다시 같은 옵션으로 컨테이너 실행
`docker run -d --network mynet -v myvol:/var/lib/mysql --name mysql_server1 -e MYSQL_ROOT_PASSWORD=1 -e MYSQL_USER=goodbird -e MYSQL_PASSWORD=1 mysql`

6. `docker run -it --network mynet --rm mysql mysql -h mysql_server1 -u goodbird -p` 으로 다시 접속하여 아까 만들었던 table이 있는지 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/26112cf7-5276-425b-85d3-7a083d3a30e5)


### wordpress mysql연동

1. mysql Dockerfile작성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/46d60c5f-d572-4ec1-a5b1-9048dec437cf)

2. mysql 이미지 파일 build `dokcer build -t gooddb .`

3. `docker run -d --network mynet --name gooddb gooddb` mysql 컨테이너 실행

4. wordpress Dockerfile작성 (반드시 DB연결 정보랑 같아야 한다.)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5f43085f-3f4e-4435-a396-5b888c84756e)

5. wordpress 이미지 파일 build `dokcer build -t gooddb .`

6. `docker run --name word --network mynet -p 8081:80 -d word` wordpress 컨테이너 실행

7. 해당 경로로 접근하기

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/517f2a48-6d96-442e-8ef8-9b73ec36bad0)

## 도커 컴포즈로 분산 애플리에키션 실행하기

### 컴포즈 파일 생성하기

1. `vi docker-compose.yml`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/d363a088-5664-4de4-a526-a00f24a2fe27)

2. `docker-compose up -d`로 컨테이너 실행

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/adb25052-4431-4e29-b595-653fb4616d97)

3. `docker-compose down` 컨테이너 종료 후 삭제

4. compose.yml파일에 apache서버도 추가

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9f08228d-7842-4797-bd7e-69272908352a)





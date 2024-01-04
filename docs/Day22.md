# Day22

## 도커 허브 등 레지스트리에 이미지 공유하기

### 도커 허브에 직접 빌드한 이미지 푸시하기

1. `docker login`으로 도커 허브에 로그인

2. `docker tag myhttpd1 goodbird0/myhttpd:1.0` 기존의 Docker 이미지명을 새로운 이름으로 변경하거나, 새로운 태그명을 붙일 때

3. `docker push goodbird0/myhttpd:1.0` 도커 Hub에 이미지 푸시하기

4. `docker pull khalinux/myhttpd:1.0` 도커 허브에 있는 이미지 Pull하기

### 도커 레지스트리 운영

1. `docker run -d -p 5000:5000 --restart always --name registry registry:2`

2. `sudo vi /daemon.json`파일 생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/daae7258-4c8c-49b4-8c59-9dcec4f39c97)

3. `docker tag myhttpd1 myregistry.local:5000/web/myhttpd:v1.0`

4. `docker push myregistry.local:5000/web/myhttpd:v1.0`

5. `docker pull myregistry.local:5000/web/myhttpd:v1.0`

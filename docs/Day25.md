# Day25

### 매니페스트파일로 mysql과 wordpress연동하기

1. mysql.yml과 wordpress.yml, mysqlservice.yml, wordpressservice.yml파일 작성

mysql.yml

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/fd0c8624-75f4-4d18-b99e-9bb1078e7cfb)

mysqlservice.yml

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a93f712d-f98f-405d-8963-d6495e201cad)

wordpress.yml

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b812a9ac-2701-4ed4-a7fa-b52a7600f6af)

wordpressservice.yml

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a385b30f-f768-4add-94da-53f7cf52557c)

2. `kubectl apply -f wordpress.yml`로 pod와 service생성


### 쿠버네티스 패키지 관리자 helm

- helm프로젝트 홈페이지(https://helm.sh/)
- 쿠버네티스 패키지 저장소(artifacthub.io)
- helm 도구 설치
  - ```curl -fsSL -o get_helm.sh 
       https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get-helm-3
       chmod 700 get_helm.sh
       ./get_helm.sh
    ```


helm install mynginx bitnami/nginx --set replicaCount=3

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

#### helm주요개념
- chart
  - helm 패키지
  - 쿠버네티스 클러스터 내에서 애플리케이션, 도구, 서비스 구동에 필요한 모든 리소스 정의
  - 설치될 떄마다 release 생성
- 저장소
  - chart르 모아두고 공유하는 곳
- 릴리즈
  - 쿠버네티스 클러스터에서 구동되는 차트의 인스턴스
  - 동일 클러스터 내에 반복 설치 가능, 매번 새로운 릴리즈 생성
 
#### helm 사용

- 변수(옵션) 확인 및 변경
  - `helm show values <저장소명>
  - 변수(옵션) 수정 후 설치시 적용 가능
  - `helm install -f 수정파일명 <저장소명> --generate-name
- 삭제
  - `helm uninstall` 또는 `delete 릴리즈명`
- 목록 확인
  - `helm list / helm repo list`

#### helm으로 kubernetes 클러스터에 배포하기

1. helm install mynginx bitnami/nginx --set replicaCount=3




kubectl create namespace wordpress

helm install mywordpress bitnami/wordpress -n wordpress

1. `kubectl create ns profana`로 네임스페이스 생성

2. `vi prom-values.yaml`로 기본설정을 바꿔주거나 install이후 kubectl `edit svc prom-kube-prometheus-stack-prometheus -n profana`로 type변경

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/39a52a69-e951-4543-9101-af414f6cf0d4)

3. `helm install prom prometheus-community/kube-prometheus-stack -f prom-values.yaml -n profana`로 클러스터에 배포

4. `kubectl get pod -n profana`와 `kubectl get svc -n profana`로 파드, 서비스 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a1e86427-8f80-4311-b895-35bc331c61cd)
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/fecb7565-601d-46f1-8af5-1e58bc230e49)

5. EXTERNAL-IP로 prometheus접속

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/7a6499d8-4fe5-4722-891d-b77a83f7597f)

6. EXTERNAL-IP로 grafana접속

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/abcf39df-95fe-4a5c-87a2-79c910185b1b)





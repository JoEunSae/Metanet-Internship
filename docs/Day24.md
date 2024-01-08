# Day24

## 쿠버네티스

**참조 자료(https://ikcoo.tistory.com/8)   (https://kubernetes.io/ko/docs/concepts/overview/)**

### 쿠버네티스(Kubernetes)란?
- 컨테이너 오케스트레이션 도구 : 시스템 전체를 통괄하고, 여러 컨테이너를 관리하는 일
- K8s라고도 부름
- 쿠버네티스는 대규모 시스템 관리에 적합 : 여러 대의 컨테이너가 여러 대의 서버에 걸쳐 실행되는 것을 전제
- 번거로운 컨테이너 생성 및 관리의 수고를 덜어주는 도구 : 도커 컴포즈와 유사하게 정의파일만 작성하면 모든 물리 서버에 컨테이너를 생성하고 관리

### 컨테이너 오케스트레이션
- 컨테이너들을 지휘하는 메인 컨트롤러가 있고 그 지휘에 맞춰 컨테이너의 배포, 관리, 확장, 네트워킹을 자동화하는 것을 말한다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/8c11f0ab-3476-4f94-9a73-24f7fd1e84b5)


### 쿠버네티스와 CNCF(Cloud Native Computing Foundation)
-  쿠버네티스 : 클라우드 네이티브 컴퓨팅 재단에서 정한 표준
-  원래 구궁에서 개발, CNCF에 기부하여 오픈소스로 전환
-  관리 기능을 강화한 버전이나 크기를 줄인 버전 등 서드파티 버전들이 발표되고 있다.
-  AWS나 Azure 및 GCP 같은 클라우드 서비스에서 커스터마이징된 쿠버네티스 서비스 제공

### 쿠버네티스 구조
- Master 노드
  - 컨테이너 실행 안함
  - 우커 노드에서 실행되는 컨테이너 관리
  - 컨테이너 엔진 설치 안됨
- Work 노드
  - 실제 서버 역할
  - 컨테이너가 실제 동작하는 서버
  - 컨테이너 엔진 설치
 - 클러스터
   - 마스터 노드와 여러 개의 워커 노드로 구성
   - 마스터 노드에 설정된 내용에 따라 사람의 개입없이 자율적으로 워커 노드 관리

### 쿠버네티스 구성요소
- Pod (1Pod 1Container가 국룰)
  - 쿠버네티스에서 관리하는 컨테이너 단위
  - 컨테이너와 볼륨을 하나로 묵은 것
  - 1개의 컨테이너 또는 여러 개의 컨테이너로 구성될 수도 있음
- Service
  - 여려 개의 파드를 하나로 관리하며, 자동으로 고정된 IP 주소를 부여받아 이 주소로 통신
  - 서비스가 분배하는 통신은 한 워크 노드 안으로 국한됨
  - 여러 워커 노드간 분배는 실제로 로드밸런서나 인그레스가 담당
- Deployment
  - 파드의 배포를 관리하는 요소
  - 파드가 사용하는 이미지 등 파드에 대한 정보를 가지고 있음
  - 레플리카세트를 관리

#### Work Node
- Pod
- Kube Proxy 
- Kubelet : 마스터 노드에서 받은 명령을 기반으로 노드 상의 컨테이너를 관리하고 실행

#### Master Node
- etcd :  Kubernetes의 상태 및 구성 정보를 저장하는 데 사용
- Kube Scheduler : 새로운 Pod가 어떤 노드에서 실행될지를 결정하는 역할을 담당하는 컴포넌트
- Kube Controller Manager :  Kubernetes 클러스터의 여러 컨트롤러를 실행하는 역할을 하는 컴포넌트
- Cloud Controller Manager : ubernetes 클러스터에서 클라우드 특화 기능을 제공하기 위한 역할을 하는 컴포넌트
- Kube API Server : Kubernetes 클러스터의 중심 컴포넌트로, 클러스터의 API를 노출하고 클러스터 내의 모든 리소스와 객체를 관리하는 서버

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3fc97a43-db1d-496f-890b-7c0aeebb39b8)

### 쿠버네티스 제어

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/77ccd314-cd7e-425a-84c2-b126ac1fc08a)


### 쿠버네티스 종류

#### 원조 쿠버네티스와 클라우드 버전
- 원조 쿠버네스트를 많이 사용하기는 하지만 직접 구축이 용이하지는 않음
- 시스템 통합 전문가에게 의뢰하는 일이 많음
- 클라우드 버전의 경우 전문적인 지식이 없어도 이용가능


### minikube
- 컴퓨터 한 대에 마스터 노드와 워커 노드를 구축하여 쿠버네티스 기능을 사용할 수 있음
- minikube설치
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start
```

- `minikube addons list`로 Minikube 클러스터에 현재 설치된 애드온(Add-ons) 목록 확인
- `minikube addons configure metallb`로 ip주소 자동 할당
-  `kubectl get pods -o wide` 현재 Kubernetes 클러스터에서 실행 중인 Pod들의 목록을 가져오고, 각 Pod에 대한 자세한 정보를 포함하여 출력
- `kubectl get svc`로 서비스 확인
- `kubectl get pod`로 파드 확인

#### kubernetes 클러스터에서 서버 배포하기

1.  Kubernetes 클러스터 내에 새로운 Deployment를 생성 `kubectl create deployment httpd --image=httpd`

2. Kubernetes 클러스터 내에 존재하는 Deployment나 Replication Controller 등의 리소스를 외부와 연결하고 해당 리소스에 대한 서비스를 생성 `kubectl expose deployment httpd --type=LoadBalancer --port=80`

3. kubectl get svc로 ip확인하여 curl로 접근

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0f5e96df-9665-429a-9022-a8f81ea4cc63)


### 매니페스트 파일
- 매니페스트 파일을 쿠버네티스에 업로드하면, 그 내용을 etcd 데이터 베이스에 '바람직한 상태'로 등록하고 서버를 그 상태로 유지
- 매니페스트 파일 작성
  - YAML 또는 JSON 형식으로 작성
  - 파드나 서비스에 대한 설정
  - 파일명은 정해져 있지 않음
- 디플로이먼트 리소스에 파드와 레플리카세트의 기능이 포합되어 있어 주로 디플로이먼트 리소스와 서비스 리소스를 많이 사용
- 매니페스트 파일 분할
  - 리소스 단위로 분할 가능
  - 하나의 파일로 작성하는 경우에는 각 리소스를 '---'로 구분
  - 리소스 단위로 나눌 때는 파일명에 리소스 구별이 되도록 이름 지정
 
#### 매니페스트 파일 작성 방법

- 매니페스트 파일의 주 항목

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/51d67ac4-13a3-4beb-a6e9-214395b7eb75)

- 리소스 설정(API 그룹 및 유형)
  - 리소스를 정의하려면 API그룹과 리소스 유형을 지정해야 함.
  - `kubectl api-resources` 명령 또는 공식 사이트에서 확인
- 메타데이터와 스팩
  - metadata : 리스소의 이름이나 레이블을 작성
  - spec : 리소스의 내용을 정의, 항목은 리소스의 유형에 따라 달라짐

#### Deployment 매니페스트 파일
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3c652ded-8144-4fc5-b170-7916a8e16da1)

#### Service 매니페스트 파일
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/663d5bc7-5255-4ea1-84ed-26d1d87eac4a)

#### 매니페스트 파일로 pod구성하기

1. vscode로 httpd.yml, service.yml 파일 작성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5970bb51-efaa-4df3-a153-16c6bfe5849f)
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/79784337-c7f7-49a7-a488-a4c7eb793d56)

2. `kubectl apply -t httpd.yml`와 `kubectl apply -t service.yml`로 pod생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/89b3afd8-0a28-44d0-8cc1-0fd2f26e0a19)
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/02d678e9-0e83-4bc1-979a-8caa0dc261e1)

3. curl로 접속

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f130c68f-4e3a-4962-a087-0b210858ca02)
 

# Day42

## MetalLB

### MetalLB란?
- Kubernetes 클러스터에서 로드 밸런서 서비스를 제공하기 위한 도구

### MetalLB주요 특징
- 로드 밸런싱 :  MetalLB는 Kubernetes 내에서 서비스에 대한 외부 노출을 담당하는 로드 밸런서 역할을 수행합니다. 서비스의 유형에 따라 Layer 2 (Data Link Layer) 또는 BGP (Border Gateway Protocol)를 사용하여 외부에서 내부로의 트래픽을 로드 밸런싱한다.
- ConfigMap사용 :  MetalLB는 Kubernetes ConfigMap을 사용하여 로드 밸런서의 설정을 관리합니다. 사용자는 ConfigMap을 통해 로드 밸런서의 IP 주소 범위를 정의하고, 해당 범위 내에서 IP 주소를 동적으로 할당받을 수 있다.
- Layer2 및 BGP : MetalLB는 두 가지 주요 모드를 지원합니다. Layer 2 모드는 ARP 프로토콜을 사용하여 로드 밸런서의 MAC 주소를 노드에게 노출하고, BGP 모드는 BGP 프로토콜을 사용하여 노드 간에 IP 주소를 공유한다.
- 통합성 : MetalLB는 Kubernetes의 네이티브 구성 및 리소스를 사용하므로 다른 Kubernetes 리소스와 조화롭게 통합된다.
- 오픈소스 :  MetalLB는 오픈 소스 프로젝트로 개발되어 커뮤니티 기여를 받고 있다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a172b790-9452-4de0-8deb-327a8c7e4495)

### MetalLB설치

1. 설치전 쿠버네티스 설정 변경 `kubectl edit configmap -n kube-system kube-proxy`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/7a691ece-a08f-469c-9fe6-4ed280a5f2d4)
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4fe36e8e-7ec4-40cd-8dda-d2941717e4cd)

2. MetalLB설치 `kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.3/config/manifests/metallb-native.yaml`

3. 아래 파일 작성하고 `kubectl apply -f new-metallb-config.yam`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/58a73c0e-64aa-44f7-ac0e-abe345106045)

4. 이후 생성된 서비스는 loadbalncer타입으로 제공

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/37ad2e71-b227-4075-96f7-5d52a5eef388)


## Service Mesh

### Service Mesh란?
- 쿠버네티스와 같은 컨테이너 오케스트레이션 환경에서 일반적으로 애플리케이션 코드와 함께 배치된 확장 가능한 네트워크 프록시 모듈로 구현
- 분산 시스템에서 서비스 간 통신을 관리하고 모니터링 하기 위한 인프라 스트럭처 계층이다.

### Service Mesh 이점
- 개발자 들은 비즈니스 로직에 집중할 수 있습니다.
- 문제를 손쉽게 인식하고 진단할 수 있습니다.
- 장애가 발생한 서비스로부터 요청을 재 라우팅 할 수 있기 때문에 애플리케이션 복구 능력이 향상된다.
- 성능 메트릭을 통해 런타임 호나경에서 커뮤니케이션을 최적화하는 방법을 제안할 수 있다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/67f1bd13-804b-4ae1-9688-a69087928e05)

### Istio설치

1. `curl -L https://istio.io/downloadIstio | sh -`로 파일 가져오기

2. 해당 디렉터리러 이동하여 환경변수 설정 `export PATH=$PWD/bin:$PATH`

3. `istioctl install --set profile=demo` istio설치

4. test를 위한 app 배포

```bash
kubectl get ns --show-labels
kubectl label namespace bookinfo istio-injection=enabled
kubectl -n bookinfo create -f samples/bookinfo/networking/bookinfo-gateway.yaml
kubectl -n bookinfo create -f samples/bookinfo/platform/kube/bookinfo.yaml
```

5. istio-ingressgateway로 접근하여 app배포 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/518e18bf-4ec7-490a-a83e-7154579e2c00)

#### kiali
- 웹 대시보드 형태로 Istio 정책을 제어하고 Istio 동작을 확인할 수 있는 기능을 지원
- Prometheus와 grafana에 연계해서 메트릭을 가져오고 대시보드에 애니메이션을 보여주기 때문에 함께 구성되어야 한다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3076c2f8-9a43-42bf-a09f-67ac4a72782b)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9dfc5540-d8d1-4e1d-97bb-7b10c0eb487e)

#### kiali설치

1. `kubectl apply -f samples/addons`로 대쉬보드 추가

2. ` istioctl dashboard kiali` 대쉬보드로 port forwarding

3. kiali 해당 포트로 접속

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/33dba167-3cd8-4e2b-be13-5a84913270d1)

# Day26

## 레드햇 OpenShift

### OKD(OpenShift Origin community Distribution Kubernetes)
- 컨테이너화된 애플리케이션을 개발하고 수행하기 위한 플랫폼
- 소규모의 데이터센터가 수천대 규모의 데이터센터로 확장이 가능하도록 설계
- 대규모 통신, 스트리밍 비디오, 게임, 인터넷 뱅킹 등 다양한 애플리케이션의 기반이 되는 기술을 통합함으로써 단일 클라우드 ,온프레미스 및 멀티 클라우드 환경에 까지 컨테이너화된 애플리케이션을 확장, 배포, 실행

 #### 쿠버네티스

- 컨테이너화된 어플리케이션의 배포, 확장, 관리 등을 자동화하기 위한 오픈소스 컨테이너 오케스트레이션 엔진
- 컨테이너는 1개이상의 워커 노드에서 실행
- 매스터 노드에서 워커 노드에 배포를 관리
- pod 단위로 컨테이너를 배포
- pod를 이용하여 컨테이너에 메타데이터를 부여할 수 있으며 여러 개의 컨테이너를 그룹화할 수 있음
- 특별한 Asset
  - service : 일련의 pod 와 액세스 방법을 정의하는 정책을 의미
  - replica controller : 한번에 실행하는데 필요한 pod 복제본 수

#### OKD4 아키텍처
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/baed195d-5893-49bf-8314-81ec6c7597e6)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b56172ba-5a7b-415f-a427-2e201dd11476)

#### OKD4 구성 오픈소스
- Cri-O : 컨테이너화된 애플리케이션을 실행하기 위한 경량 컨테이너 런타임
- Podman : 컨테이너를 관리하는 도구로, Docker와 유사한 기능을 제공하지만, Docker의 데몬 프로세스 없이 동작하며 루트 권한 없이도 컨테이너를 다룰 수 있도록 설계
- Skopeo : 컨테이너 이미지 간에 이미지를 복사하고 검사하며 여러 저장소 간에 이미지를 전송하는 데 사용되는 명령줄 도구
- Buildah : 컨테이너 이미지를 빌드하기 위한 명령줄 도구로서, 컨테이너화된 애플리케이션을 구축하는데 사용
- Operator : kubernetes에서 사용되는 컨테이너 오케스트레이션 시스템에서 애플리케이션을 배포, 관리 자동화하기 위한 사용자 정의 컨트롤러이다.
- Prometheus : 컨테이너화된 애플리케이션 및 MSA에서 사용되는 오픈 소스 시스템 모니터링 및 경고 도구
- Grafana : 오픈 소스의 데이터 시각화 및 모니터링 플랫폼으로, 다양한 데이터 소스로부터 데이터를 가져와 다양한 그래프 및 대시보드로 시각적으로 표시할 수 있는 도구
- Elastic Search : 오픈 소스의 분산형 검색 및 분석 엔진으로, 대량의 데이터를 신속하게 검색, 분석 및 시각화 라수 있도록 설계
- FluentD : 오픈 소스의 데이터 수집 소프트웨어로서, 다양한 소스에서 로그 데이터를 수집, 전송 및 처리하는데 사용
- Kibana : Elasticsearch와 함께 사용되는 오픈 소스의 데이터 시각화 및 대시보드 플랫폼
- Jenkins : 오픈 소스의 지속적 통합 및 지속적 배포 도구
- Tekton : Kubernetes환경에서 사용되는 오픈 소스의 CI/CD 프레임워크
- Istio : 서브스 망*(Mesh) 기반의 MSA에서 서비스 간 통신, 보안, 관측성 및 통제를 제공하는 오픈 소스 플랫폼
- Kiali : 서비스 메시 관리를 위한 오픈 소스 웹 기반 플랫폼 중 하나로, 특히 Istio와 같은 서비스 망 솔루션과 통합되어 사용
- Jaeger : 분산 시스템에서의 트랜잭션 추적을 제공하는 오픈 소스 분산 트레이닝 시스템
- Knative : kubernetes 위에서 서버리스 애플리케이션을 구축하고 배포하기 위한 오픈 소스 플랫폼
- Keda : kubernetes 환경에서 이벤트 기반의 자동 스케일링을 지원하는 오픈 소스 프로젝트
- S2i : 소스 코드를 컨테이너 이미지로 변환하는 오픈 소스 도구
- Ceph : 대규모의 분산 스토리지 시스템을 제공하는 오픈 소스 프로젝트
- Rook : 클라우드 네이티브 환경에서 스토리지를 관리하기 위한 오픈 소스 프로젝트, 특히 kubernetes 클러스터에서 사용
- OVS : 가상화 및 컨테이너 환경에서 네트워크 가상화를 지원하기 위한 오픈 소스 가상 스위치
- OVN : 네트워크 가상화 및 SDN을 위한 오픈 소스 프로젝트로서, Open vSwitch위에서 동작하는 가상 네트워킹 솔루션
- KubeVirt : kubernetes클러스터에서 가상 머신을 관리하고 실행하기 위한 오픈 소스 프로젝트

### FCOS(Fedora CoreOS)
- 차세대 단일 목적의 컨테이너 OS 기술
- Container Linux의 자동화된 원격 업그레이드 기능 지원
- 마스터 노드의 기본 OS이며, 클러스터 시스템 워커 노드의 기본 OS

#### 주요기능
- Fedora 리눅스 기반 (RPM, systemd, fedora 커널)
- 기존의 Fedora 엄격하게 관리되도록 설계 (원격 관리, 시스템 설정 변경 최소화)
- Cri-O 컨테이너 엔진 내장
- 컨테이너 제어도구(Builda, Scopio, podman 등)
- rpm-ostree 시스템을 사용한 트랜잭션 업그레이드 제공
- Machine Config Operator 를 통한 OS 업그레이드

### Operator
- 쿠버네티스 환경을 지속적으로 확인하고, 현재 상태를 사용하여 실시간으로 의사결정
- 쿠버네티스 어플리케이션을 패키징, 배포, 관리하는 방법

#### 기능
- 설치 및 자동 업그레이드
- 모든 시스템 구성요소의 지속적인 상태 확인
- OKD 구성요소 및 ISV(Independent Software Vendor) 컨텐츠에 대한 OTA(Over-the-air) 업데이트
- 현장 엔지니어의 축적된 지식을 모든 사용자에게 전파할 수 있는 공간

### OKD4 모니터링 구성요소
- 클러스터 모니터링 Operator : Kubernetes 클러스터에서 애플리케이션 및 인프라스트럭처의 모니터링을 자동화하기 위한 Kubernetes Operator 중 하나
- Prometheus Operator :  Kubernetes 클러스터에서 Prometheus를 관리하고 설정하기 위한 Kubernetes Operator 중 하나
- Prometheus Adapter : Kubernetes에서 사용되는 Custom Metrics API에 Prometheus에서 수집한 지표(metric)를 노출시키기 위한 도구 중 하나
- AlertManager :  Prometheus 생태계에서 사용되는 알람 관리 및 라우팅 도구로, Prometheus로 수집된 지표에 기반하여 생성된 알람을 효율적으로 관리하고 알림을 전달하는 역할
- kube-state-metrics 에이전트 : Kubernetes 클러스터의 상태 및 메타 데이터를 수집하여 Prometheus에서 사용할 수 있는 메트릭으로 변환하는 에이전트
- Openshift-state-metrics 에이전트 :  Kubernetes 클러스터의 상태와 관련된 메트릭을 수집하고 Prometheus에서 사용할 수 있는 형식으로 변환하는 에이전트
- Node-export 에이전트 : 호스트 머신의 리소스 사용량 및 성능 지표를 수집하여 Prometheus 서버로 전송하는 역할
- Thanos Queier :  Prometheus의 쿼리 언어를 확장하고 대규모 Prometheus 기반 메트릭 시스템에서 작동할 수 있도록 설계된 도구
- Grafana
- telemeter client

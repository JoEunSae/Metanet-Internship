# Day40

## 핵심 인프라 보호

### NSG(네트워크 보안 그룹)
- 가상 네트워크의 리소스에 대한 인바운드 아웃바운드 네트워크 트래픽을 허용하거나 거부하는 데 사용하는 가상 방화벽 역할의 보안 계층
- 네트워크 보안 그룹은 서브넷이나 네트워크 인터페이스에 적용할 수 있으며 인바운드 아웃바운드 네트워크 트래픽 유형을 필터링하기 위해 보안 규칙을 작성한다.

#### 기본 보안 규칙
- 기본 규측은 네트워크 보안 그룹을 배포할 때 만들어지며 제거하지 못한다.
- 인바운드 기본규칙
  - 가상 네트워크와 Azure 부하 분산 장치에서 들어오는 인바운드 트래픽을 제외한 모든 인바운드 트래픽을 거부한다.
- 아웃바운드 기본규칙
  - 인터넷과 가상 네트워크에 대한 아웃바운드 트래픽만 허용하고 그 외는 모두 거부한다.
 
#### 네트워크 보안 그룹 설정
- 보안그룹
  - 서브넷과 네트워크 인터페이스에서 인바운드/아웃바운드 트래픽을 필터링하기 위해 사용자 지정 보안 규칙을 만든다.
- 네트워크 인터페이스
  - 네트워크 보안 그룹을 네트워크 인터페이스에 연결하면 가상 머신으로 들어오고 나가는 트래픽을 제어할 수 있다.
- 서브넷
  - 네트워크 보안 그룹을 연결하면 해당 서브넷에 있는 모든 가상 머신으로의 트래픽 흐름을 제한할 수 있다.

### Azure Bastion 서비스
- 외부에서 RDP나 SSH를 통해 액세스하는 가상 머신의 보안 위협을 완화하기 위해 Azure 포털과 TLS 연결을 수립한 후 Azure 내에서 RDP나 SSH로 해당 가상 머신을 안전하게 액세스할 수 있도록 하는 관리형 Paas 서비스

#### Bastion 서비스의 이점과 동작 방식
- Bastion 서비스를 배포하면 RDP와 SSH를 통해 액세스하는 데 필요했던 공용 IP 주소를 제거해 클라우드 인프라의 공격 면적을 줄일 수 있다.
- Bastion 서비스는 전용 서브넷에 배포되고 공용 IP 주소를 노출하지만 SSL 연결만 수락하고 RDP와 SSH 연결은 허용하지 않는다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/998ae438-f4a8-4876-8587-ec8b500929fb)

## ArgoCD

### GitOps

#### GitOps란?
- Git 저장소를 사용하는 소프트웨어 배포 접근 방식이다.
- 하나의 목표를 가진 운영 프레임워크 애플리케이션 개발에 사용되는 DevOps 모범 사례를 인프라 장도화 프로세스에 적용하는 것

#### GitOps 특징
- 전체 시스템은 코드로 설명한다. ( IaC )
- 시스템의 원하는 상태는 Git에서 버전 관리한다.
- Git에서 변경 사항을 시스템에 자동으로 적용할 수 있다.
- 자동화는 시스템이 신뢰할 수 있는 위치에 설명된 상태와 항상 일치하는지 확인한다.

### ArgoCD란?
- GitOps 방식으로 관리되는 Manifest(yaml)파일의 변경사항을 감시하며, 현재 배포된 환경의 상태와 Github Manifest파일에 정의된 상태를 동일하게 유지하는 역할을 수행
- ArgoCD는 쿠버네티스를 위한 CD(Continous Delivery)툴이다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/d1dc9169-529d-4d94-8981-c532f5d511c6)

### Calico CNI

#### Calico CNI란?
- 컨테이너, 가상 머신 및 기본 호스트 기반 워크로드를 위한 소스 네트워킹 및 네트워크 보안 솔루션이다.
- Kubernetes, OpenShift, Mirantis Kubernetes Engine(MKE), OpenStack 및 베어메탈 서비스를 포함한 광범위한 플랫폼 지원한다.
- Calico의 eBPF 데이터 플레인을 사용하든 Linux의 표준 네트워킹 파이프라인을 사용하든 Calico는 진정한 클라우드 네이티브 확장성과 함께 놀랍도록 빠른 성능을 제공한다.
- Calico는 공용 클라우드나 온프레미스, 단일 노드 또는 수천 개의 노드 클러스터에서 실행되는지 여부에 관계없이 개발자와 클러스터 운영자에게 일관된 경험과 기능 세트를 제공한다.

#### Calico 설치

1. 우선 `sudo kubeadm init --pod-network-cidr=172.20.0.0/16 --upload-certs --control-plane-endpoint=k8s | tee kubeadm.out
Kubenetes`로 초기화

2. `kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.0/manifests/tigera-operator.yaml`로 Calico Operator설치

3. `wget https://raw.githubusercontent.com/projectcalico/calico/v3.27.0/manifests/custom-resources.yaml`으로 cusotm manifest파일을 가져와 cidr부분 init시 대역으로 수정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/64c5a3b1-12f1-4f6b-b4e9-65b46c91aa3e)

4. `kubectl apply -f custom-resources.yaml`로 수정한 manifest파일 적용

5. calico pod와 svc생성 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/744f95c4-64bd-4684-a8f0-bc0a4ebe2a2a)

# Day37

## Azure

### 가상 네트워크
- SDN과 클라우드의 이점을 통해 뛰어난 확장성
- 프라이빗 네트워크
- 가용성
- 효율성 제공
- 안전한 통신을 위한 트래픽 격리
- 하이브리드 연결
- 기본 outbound 인터넷 가능
- 인바운드 공용IP 주소나 

#### 서브넷
- 네트워크 성능과 속도가 향상된다.
- 네트워크 정체를 줄인다.
- 네트워크 보안을 향상시킨다.
- 네트워크가 비대해지지 않게 한다.
- 관리가 용이하다.

#### 가상 네트워크 만들기

1. 기본사항 
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/bf7f698b-ddbe-41a2-9367-42b153eeb299)

2. IP주소
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/90b03c28-bedc-4ace-a079-ae12223d617a)

3. 서브넷 추가
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/22efb2b0-523e-4352-b952-d7139bb6f771)

### Azure Virtual Machine

#### 가상 머신 유형
- Azure 가상 머신 : Azure에서 호스팅 하는 가장 많이 사용하는 일반적인 형태의 가상 머신을 만들 때 사용하는 옵션
- 사전 설정 구성이 포함된 Azure 가상 머신 : 워크로드에 기반한 사전 설정이 포함된 가상 머신을 만들 때 사용하는 옵션
- Azure Arc 가상 머신 : Hyvrid형태로 관리 (op-premise)
- Azure VMware 솔루션 가상 머신 : Azure VMware Solution 프라이빗 클라우드를 만들어 Azure Arc에 온보딩한 후 AVS 가상 머신을 만듭니다.

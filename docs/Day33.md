# Day33

## 프로젝트 이어서 진행

### 클라우드 벤더와 서비스 제품 비교

#### AWS,Azure,GCP 가격 비교
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/28231066-119a-4422-9700-b31db3c82b93)

#### AWS,Azure,GCP 성능 비교
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/843ddd12-6a51-4256-bd32-d210a5f45be6)
- 데이터를 인식하는 속도 및 성능 면에서 Azure가 1위, 10KB 크기 데이터를 업로드해 읽고 쓸때 속도에서 AWS S3에 비해 쓰기의 경우 56%, 읽기의 경우 39% 빠른 속도를 보였다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/c563bbfc-a411-47ba-9f28-8e9d6ea28ae6)
- 에러 발생률 부분에서는 AWS, Azure, GCP모드 0%를 기록했고, 읽기 작업 시 Azure가 유일하게 에러가 발생하지 않았다. 

### 클라우드 업계 시장 점유율
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/bdf6c4f4-9aa6-4da5-a374-487aa09e80bb)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9d26cd63-1100-4ebb-aa4b-b144010d1b4f)

### 클라우드 구현 주요 기술

#### Virtualization
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/634186b7-d65d-4999-9c5a-7a42af381e4c)

- Native/Baremetal Virtualization
  - 네이티브 혹은 베어메탈 하이퍼바이저를 이용하는 가상화.
  - 하이퍼바이저가 하드웨어를 직접 제어하고 그 위에 게스트 운영체제(Guest OS)를 올리는 방식
  - 베어메탈 하이퍼바이저는 자신만의 디바이스 드라이버를 가지고 입출력, 프로세싱, OS 관련 컴포넌트들과 직접 교류하여 처리함.
  - 더 나은 퍼포먼스, 확장성, 그리고 안정성을 가지게 된다.
  - 하이퍼바이저에는 제한된 숫자의 디바이스 드라이브가 설치 될 수 있으므로, 그만큼 하드웨어 호환성이 제한될 수 있다.
- Hosted Virtualization
  - 전통적인 운영체제위에 하이퍼바이저를 실행하고, 이 하이퍼바이저 위에서 게스트 운영체제를 실행하는 방식.
  - 기존에 사용하던 호스트 운영체제 위에, 애플리케이션을 실행 하듯이 게스트 운영체제를 올릴 수 있음
  - 호스트 운영체제 위에 게스트 운영체제를 작동시키기 때문에 필요 이상으로 CPU나 메모리 사용이 증가하는 오버헤드가 발생합니다.
- Container Virtualization
  - Host OS가 가진 리소스를 적게 사용하며, 필요한 프로세스만을 실행하는 방식
  - 컨테이너는 호스트 시스템의 커널을 다른 컨테이너들과 공유한다
  - Application을 구동할 수 있는 환경만을 가상화한다. 즉, CPU와 Memory 영역 등을 가상화하고 구동하는데 필요한 운영체제나 라이브러리는 호스트 시스템과 공용으로 사용

#### 분산처리
- 컴퓨팅 분산처리 기술은 '데이터를 병렬처리 하여 데이터 처리 속도를 높이는 기술’이다. 옛날에는 대용량 데이터를 처리하려면 고사양의 CPU와 대용량 메모리가 탑재된 서버가 필요했다. 분산처리 기술을 통해 데이터를 하나의 서버가 아닌,
여러 대의 서버에 나누어서 '병렬'로 처리할 수 있다.  이렇게 여러 개의 서버를 결합해서 하나의 컴퓨터로서 보이게 하는 기술을 클러스터링이라고 한다.분산처리는 대용량 데이터와 트래픽 발생하는 앱, 웹 서비스, 게임서비스에 유용하게 쓰인다. 

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/39601513-bd9b-4a60-82f3-8962d12b45ca)

#### Serverless
-  사용자는 스케일링, 업데이트, 보안 등 런타임 관리와 운영에 대해 시간을 소모하지 않고 핵심 제품에 집중할 수 있습니다.
- 애플리케이션은 자동으로 확장될 수 있고, 개별 서버 단위가 아닌 사용단위(처리량, 메모리)를 설정/해제하여 용량을 조정할 수 있습니다
- 사용자가 없다면 자원을 할당하지 않고 대기하다가 요청이 들어오면 그 때 자원을 할당해서 요청을 처리하고 다시 대기 상태로 들어가게 됩니다. 자원을 효율적으로 사용할 수 있는 것입니다.

### 클라우드 보안
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3afea663-3da4-4166-a5d6-927ac3cb0a1a)

- 클라우드는 항상 안전한가?
  - 클라우드는 여러 장점이 있지만 보안은 벤더사에 의해 좌지우지 되기 때문에 높은 보안을 요하는 데이터는 주의가 필요함 
  - 클라우드 보안을 위해 각 벤더사는 공통적으로 ＂공동 책임 모델＂을 통해 고객과 CSP가 함께  보안을 책임 지게 한다.

#### AWS 공동 책임 모델
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/215356e6-40a3-41ce-8f65-458b2f816aac)
- AWS는 일부 객체의 보안을 책임
- 객체의 보안은 고객이 전적으로 책임
- AWS는 인프라 내의 결함을 패치하고 수정할 책임
- 고객은 게스트 OS 및 애플리케이션에 패치를 적용할 책임
- AWS는 인프라 장치의 구성을 유지 관리
- 고객은 자신의 게스트 운영체제, 데이터베이스 및 애플리케이션을 구성할 책임

#### Azure 공동 책임 모델
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/80d960c8-ad5c-4b4b-9dc5-dcb382b5c667)

#### Azure 클라우드 보안을 위한 5가지 모범 사례
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/e0a565ba-c9b5-4c70-8090-e1ce90af6121)




















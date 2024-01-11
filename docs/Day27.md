# Day27

## OpenShift
- Kubernetes를 기반으로 한 컨테이너 오케스트레이션 플랫폼으로, Kubernetes의 핵심 기능을 포함하면서도 다양한 추가 기능과 도구를 제공

### 주요기능

1. Developer-Centric Experience
- OpenShift는 개발자 중심의 플랫폼으로 개발자가 애플리케이션을 빠르게 구축, 테스트 및 배포할 수 있는 기능을 제공한다.
- 소스 코드의 변화를 자동으로 감지하고 CI/CD (Continuous Integration/Continuous Deployment) 파이프라인을 설정할 수 있다.

2. Source-to-Image (S2I)
- OpenShift는 S2I라는 도구를 제공하여 소스 코드 및 빌드 설정에서 Docker 이미지를 생성할 수 있습니다. 이는 개발자가 Docker 이미지를 명시적으로 작성하지 않아도 되게끔 도와준다.

3. Web Console
- OpenShift는 웹 기반의 그래픽 사용자 인터페이스를 제공하여 클러스터 및 애플리케이션 관리를 용이하게 한다.

4. Developer and Operations Collaboration
- 개발자와 운영팀 간의 협업을 강화하기 위해 OpenShift는 더 쉬운 통합 및 커뮤니케이션을 지원한다.

5. Integrated CI/CD Pipelines
- OpenShift는 Jenkins와 같은 CI/CD 도구를 통합하여 애플리케이션의 지속적인 통합 및 배포를 쉽게 설정할 수 있다.

6. Security Features
- OpenShift는 RBAC (Role-Based Access Control), 네트워크 정책, 보안 컨텍스트 제한, 이미지 스캐닝 등의 기능을 통해 강력한 보안을 제공

7. Service Mesh Integration
- OpenShift는 서비스 메시 기술을 통합하여 마이크로서비스 기반 애플리케이션의 효율성과 통신을 관리할 수 있다.

8. Automated Scaling and Load Balancing
- OpenShift는 자동 스케일링 및 로드 밸런싱을 지원하여 애플리케이션의 성능과 가용성을 최적화할 수 있다.

9. Catalog of Pre-built Images and Templates
- OpenShift는 미리 빌드된 컨테이너 이미지 및 애플리케이션 템플릿의 카탈로그를 제공하여 개발자가 효율적으로 애플리케이션을 시작할 수 있도록 도와준다.

### kubernetes와의 차이

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/54a284ad-bf71-4d6b-8c3a-f245eba0f05f)


1. 상업 지원 및 추가 기능
- Kubernetes: Kubernetes는 오픈 소스 프로젝트로서, 커뮤니티에 의해 개발되고 유지보수됩니다. 상용 서비스 및 지원은 여러 업체에서 제공
- OpenShift: Red Hat은 OpenShift를 상용 제품으로 제공하며, Red Hat의 기술 지원 및 추가 기능, 보안 업데이트, 개발 도구 등을 포함

2. 설치 및 관리
- Kubernetes: 순수한 Kubernetes를 설치하고 관리하는 것은 일부 사용자에게는 복잡할 수 있습니다. 그러나 여러 배포 옵션이 있다.
- OpenShift: OpenShift는 Kubernetes를 기반으로 하지만, 설치 및 관리를 단순화하기 위해 추가 도구 및 프로세스를 제공한다.

3. 개발자 도구 및 경험
- Kubernetes: Kubernetes는 주로 운영자 중심의 플랫폼이며, 개발자가 사용하기 위해서는 몇 가지 추가 도구 및 설정이 필요할 수 있다.
- OpenShift: OpenShift는 개발자 중심의 플랫폼으로 개발자 친화적인 기능과 통합된 CI/CD 도구, 개발 환경 관리 기능 등을 제공한다.

4. 보안 및 정책 관리
- Kubernetes: Kubernetes는 기본적인 보안 기능을 제공하지만, 일부 고급 보안 기능이 부족할 수 있다.
- OpenShift: OpenShift는 Red Hat의 보안 역량을 활용하여 추가적인 보안 및 정책 관리 기능을 제공한다.

5. 컨테이너 런타임
- Kubernetes: Kubernetes는 컨테이너 런타임에 대한 명시적인 제약이 없습니다. 따라서 다양한 런타임을 지원
- OpenShift: OpenShift는 주로 Docker 컨테이너 런타임에 중점을 둔다.

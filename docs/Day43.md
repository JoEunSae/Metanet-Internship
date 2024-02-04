# Day43

## IaC(Infrastructure as Code)
- 인프라 코드 작성/배포/업데이트
- 기존 인프라 구성 및 운영 방식에서 코드로 관리하는 인식의 전환이 필요
- 서버,스토리지,네트워크,데이타 베이스,로그 관리,app 설정,테스트/배포 자동화 포괄

### 인프라 자동화의 변화
- 매뉴얼: 인프라 정보,구성 방법,Arch.를 문서화 —> 재사용성,버전 관리가 어려움
- 스크립트: 단순 반복 작업을 자동화
- VM : Hypervisor에 의존,골든 이미지 백업(snapshot)--> VM외 작업은 여전히 수동
- 클라우드 인프라: 필요 시점에 프로비저닝 하고 소유 개념이 아닌 리스(서비스) 개념으로 사용,클라우드 제공자마다 API가 다르다.
- 컨테이너: VM 이미지 보다 이식성이 좋고 가볍다. 앱 배포 자동화에 많이 사용

### 코드형 인프라 도구 범주
- 애드혹 스크립트
- 구성관리 도구
- 서버 Template
- 서버 프로비저닝 도구

#### 애드혹 스크립트
- 스크립트 언어(shell,python,ruby 등)로 작성하여 대상 시스템에서 실행
- 대중적인 프로그래밍 언어
- 모든 것을 직접 개발(API 지원 없음)
- 수많은 리소스 관리시 코드가 복잡해지고 가독성이 떨어지며 유지보수가 어려운 스파게티 코드가 될수 있음
- 작은 규모/단발성 작업에 적합
- 대규모 인프라 관리에 부적합

#### 구성관리 도구
- Chef,puppet,ansible,salt 등
- 스크립트 도구보다 많은 장점을 갖음
- 장점
  - 코딩 규칙:문서화/변수 정의/파일배열 구조 등 일관성 있는 구조로 가독성이 좋다.
  - 멱등성:같은 코드로 반복적으로 적용시 수행 횟수와 상관 없이 항상 동일 결과 값이 나온다는
  - 의미—> 서버 상태를 정의하여 항상 같은 상태를 유지하도록 작업을 수행
  - 분산형 구조: 대규모 분산환경의 서버 구성을 일관성 있게 유지 관리하기 위한 목적으로 설계

#### 서버 프로비저닝 도구
- 테라폼,AWS CloudFormation,Openstack Heat 등
- 인프라 리소스(서버,네트워크,데이타 베이스,스토리지,라우팅 정책,SSL 인증서,방화벽 등)를 구축(오케스트레이션)하기 위한 도구
- 서버 템플릿과 함께 사용하여 프로비저닝 시간을 단축하여 Immutable Infra 구축이 가능

### IaC 선택시 고려사항
- 인프라 구성 관리 vs 인프라 배포(프로비저닝) 도구
  - ex) 서버 template 도구+프로비저닝 도구,프로비저닝 도구+구성 관리 도구
- 절차 지향적 vs 선언형 접근방식
- 가변적인 인프라(CM) vs Immutable Infra (새버전에 대한 이미지를 만들어 배포: salt)
- Master 유무
- Agent 유무
- Community 규모
- 기술 성숙도 : 도구마다 제공 시기와 최근 버전 정보로 비교—>안정성,호환성에 영향

### IaC 도구들 비교

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4faedda4-44f3-40f7-aed6-aa990ec37756)


## Terraform

### 특징
- Go 언어로 설계된 오픈 소스 도구
- 하나의 binary로 이루어짐
- 다양한 플랫폼 지원: AWS,GCP,Azure,Openstack,VMware 등의 리소스들을 프로비저닝
- 하나의 도구로 다양한 클라우드의 인프라를 관리할 수 있다.
- 입.출력 변수 사용 가능
- 모듈화 가능
- 다양한 구문 지원(조건/반복 등)
- 코드는 HCL(HashiCorp Configuration Language)로 작성
- 확장자 .tf 
- vim,sublimeText,Atom,VS code,IntelliJ에서 문법 하이라이트 기능 지원(HCL or Terraform 검색)

### Terraform 제공 유형
- On-premise : Terraform open 소스 binary 형태로 가장 널리 사용
- SaaS : Hashcorp에서 관리형으로 제공하는 서비스 형태(Terraform cloud)
- Private Install :Terraform Enterprise로 인터넷이 격리된 환경에서 사내망 관리 목적의 서버형 설치

### Terraform 설치

1. 윈도우용 terraform설치

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/78577c7d-15be-43d1-866f-82106e2e9df2)

2. 환경변수 추가

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b167ece1-6505-4ce0-b773-c685a8181540)

3. cmd에서 terraform설치 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/be3e0a56-9226-4ba0-849a-4bfc055718ab)

4. VSCode에서 작업하기 위해 HashiCorp HCL Extension추가

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/79dba394-9c5e-4a4e-85b8-9aab341a00a3)

### Terrform 커맨드
- init : 작업 디렉토리 초기화 및 다른 명령어 실행 준비
- validate : 구성의 유효성 검사
- plan : 현재 구성에 필요한 변경 사항 표시
- apply : 인프라 생성 또는 업데이트
- destroy : 생성된 인프라 제거

### Test를 위 한 main.tf작성

```tf
resource "local_file" "abc" {
  content  = "abcdef!"
  filename = "${path.module}/abc.txt"
}
```

1. 작업 디렉토리 초기화를 위한 `terraform init`수행

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0f4f78d2-5b2d-47a7-af5c-8699d9586248)

2. `terraform validate`로 문법 체크

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/60205994-8b6c-49d4-91f6-e9b8e76c31c6)

3. `terraform plan`으로 이전 구성과 현재 구성 비교

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/503750e4-4586-472a-8154-8f39ed5df6bb)

4. `terraform apply`로 인프라 생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f5bc4b40-550f-4cba-86af-3f90dc47183b)

5. 파일생성 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/8168ec6a-5c15-44e5-bf6c-3d5800b80e94)

6. `terraform destroy`로 인프라 삭제

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/87dda4f2-c958-44a2-a02f-8214d432140a)

**`terraform fmt`로 코드 자동 재배치**

### Terraform으로 인프라 AWS에 배포

1. AWS에 배포를 위한 사용자 액세스키 발급

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/cfd3780a-de55-4cc7-9f8e-91c422fd033e)

2. AWS CLI설치

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/08d21692-097d-46d0-a0ee-e7213bd620f0)

3. aws configure로 aws cli 로그인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0bcacf6c-1f9d-4df9-a5c0-610e22d9712c)

4. main.tf작성 (여기서 ami는 aws에서 ubuntu ami id확인)

```tf
provider "aws" {
 region = "ap-northeast-2"
}
resource "aws_instance" "web" {
 ami = "ami-0f3a440bbcff3d043"
 instance_type = "t3.micro"
 subnet_id = "subnet-0719172cdc66b2caf"
}
```

5. `terraform init`으로 디렉터리 초기화

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/1f8d652f-a171-4abe-98f6-0d48d1dad014)

6. `terraform apply`으로 aws에 배포

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6444f589-8b63-43a6-97ca-287b9d8eb8e9)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2b20f355-a1cf-40c6-a441-9174d9f7b360)

### Terraform으로 인프라 Azure에 배포하기

1. 'az login`으로 azure cli 로그인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/94c20177-ddb4-4622-86a8-f743a34e6bc0)

2. test를 위한 providers.tf, main.tf, variables.tf 작성

```tf
#providers.tf
terraform {
    required_providers {
        azurerm = {
            source = "hashicorp/azurerm"
            version = "~>3.0"
        }
        random = {
            source = "hashicorp/random"
            version = "~>3.0"
        }
    }  
}
provider "azurerm" {
    features {}
}
```

```tf
#main.tf
resource "random_pet" "rg_name" {
    prefix = var.resource_group_name_prefix
}
resource "azurerm_resource_group" "rg" {
    location = var.resource_group_location
    name = random_pet.rg_name.id
}
```

```tf
#outputs.tf
output "resource_group_name" {
    value = azurerm_resource_group.rg.name
}
```
3. `terraform init`으로 초기화

4. `terraform apply`로 인프라 배포

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b5fce969-2829-451d-bc06-4d8a30462635)

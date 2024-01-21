# Day29(MiniProject2)

## 요구사항
1. 리눅스 VM 구성
2. 컨테이너+쿠버네티스 환경 구축
3. 웹사이트 구축 - 자유
4. 선택 : 웹 사이트의 상태 및 메트릭 모니터링

## 프로젝트 계획서
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/01521598-c35d-4a65-8533-ff4e4e9d606c)



## 웹 사이트 트래픽 알람, 모니터링

1. VMware에 Ubuntu설치
- RAM : 8G
- CPU : 4
- Memory : 45G

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f65f0926-26c2-4635-b978-62434039b258)

2. Docker Install

3. Minikube Install
- ```
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  sudo install minikube-linux-amd64 /usr/local/bin/minikube
  minikube start
  ```
- minikube addons list로 Minikube 클러스터에 현재 설치된 애드온(Add-ons) 목록 확인
- minikube addons configure metallb로 ip주소 자동 할당
- kubectl get pods -o wide 현재 Kubernetes 클러스터에서 실행 중인 Pod들의 목록을 가져오고, 각 Pod에 대한 자세한 정보를 포함하여 출력
- kubectl get svc로 서비스 확인
- kubectl get pod로 파드 확인

4. 패키지 형태로 받기 위해 Helm Install
- ```
   https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get-helm-3
   chmod 700 get_helm.sh
   ./get_helm.sh
  ```



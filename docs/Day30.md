# Day30

## 프로젝트 이어서 진행

1. `helm list / helm repo list` 로 helm list 와 repo확인

2. Nginx설치를 위한 bitnami repository설치

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/74e643b9-2033-4dbf-81e2-a966a3ad4387)
- `helm repo add https://charts.bitnami.com/bitnami`

3. 파드를 관리 하기 위한 namespace생성
`kubectl create namespace project`

4. bitnami repo로 부터 helm으로 Nginx/Nginx-export설치 `helm install my-nginx bitnami/nginx -n project --set service.type=LoadBalancer --set metrics.enabled=true`
- `--set service.type=LoadBalancer`로 Nginx배포와 동시에 LoadBalancer타입으로 하여 접근가능하도록
- `--set metrics.enalbed=true`는 bitnami의 nginx는 nginx와 nginx-export가 같이 하나의 파드로 함께 생성 가능
- `kubectl get pod -n project`와 `kubectl get svc -n project`로 nginx와 nginx-ecport 파드와 서비스 생성 확인
  
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a36bfa62-f6f6-41e2-855d-20c61701dc9f)


5. 


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
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f7a20d47-c36c-401f-ae6e-3cbf16719ac6)
Nginx는 80포트 Nginx-Export는 9113포트로 생성된것을 확인

5. Prometheus설치를 위한 repository설치 
- `helm repo add https://prometheus-community.github.io/helm-charts`
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b4c5d228-c5e7-42bc-ba96-2e0f75276713)

prometheus-communiy repository는  Prometheus, Prometheus-Alertmanaget, Node-Export가 포함되어 있다.

6. repo로 부터 Prometheus, Prometheus-Alertmanaget, Node-Export설치
- `helm install my-prometheus prometheus-community/prometheus -n project --set service.type=LoadBalancer`
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/be333534-096a-419f-9b85-e0dce8f1b606)

7. Grafana설치를 위한 repository설치
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/ee2016cb-b003-427d-b920-51105e67bb2c)
- `helm repo add https://grafana.github.io/helm-charts`

8. repo로 부터 Grafana설치 `helm install my-grafana Grafana/grafana -n project --set service.type=LoadBalancer`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/247c78ec-14db-4d9c-835e-ea0272f45f56)
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/ac154c78-5856-47a9-bd58-cddc2bec04e1)

9. Prometheus에서 Nginx-Export target을 설정하기위해 values.yml파일을 가져온다
- `helm show values prometheus-community/prometheus > values.yml`

10. values.yml파일을 가져와 target으로 nginx-export를 추가해준다.
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/16fcad2b-0685-4c23-87a5-f24851143ac4)

11. prometheus에 접속해서 target확인
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/75eefd15-4719-4ac5-8714-30b583c64072)

12. 경고를 보내기 위한 alertmanager도 values.yml파일에 target설정
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4d44e54d-adb7-415b-875a-a65ed91f2f4e)





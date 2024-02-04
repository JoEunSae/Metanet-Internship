# Day41.md

## ArgoCD

### ArgoCD설치

1. `kubectl create namespace argocd`로 namespace생성

2. `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`로 argocd생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/200f6ab3-213d-41aa-a15d-a0395808239a)

3. argocd CLI설치

```bash
sudo curl -sSL -o /usr/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo chmod +x /usr/bin/argocd
```

4. ` kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'`으로 argocd-server nodeport타입으로

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/ce38a36d-4a89-4957-a33d-995c7b48873c)

5. ` kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`로 비밀번호 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9154be6d-f431-49ea-9009-2f246654941b)

6. 해당 포트로 argocd 접속

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6cb78fb4-98ae-47f6-b514-014301715ef1)

7. 아이디는 admin 비밀번호는 아까 확인 비밀번호로 로그인

8. user info에서 비밀번호 변경

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/707bfe8f-8b7c-4891-b6b7-7c5b38e1e061)

### ArgoCD와 Github연동

1. 연동할 Github Repository생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/26cb78cf-94b3-4609-bef9-11416f8be7c6)

2. 연동할 `git clone https://github.com/JoEunSae/argocdtest.git`로 repository clone

3. nginx서버 배포 ` kubectl create deploy nginx --image nginx --dry-run=client -o yaml > nginx_deploy.yaml`

4. `git config --global user.email "gjsl1945@naver.com"` 전역(global) 설정을 변경하므로 해당 사용자의 모든 Git 프로젝트에서 동일한 이메일 주소가 사용

5. git에서 key 발급

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0660aa67-51e9-4ee0-94f8-2ee36dc1d8e9)

6. ArgoCD에서 app생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b78e3e61-0497-4a1a-8a87-f0ed1c2d14a5)

7. `vi nginx-deploy.yaml`로 replicas: 4 로 수정

8. `git commit -am "modified replicas=4"`로 변경사항 커밋

9. `git push`로 git에 push

10. 파드확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3f87176f-d5e6-4122-974b-51779ad0cce9)

11. argocd dashborad에 반영확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b55ab20c-01de-41f5-8e35-8e15bb5adda5)


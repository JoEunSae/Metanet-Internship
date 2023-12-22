# Day15

### 지난시간 복습

변수명="값"

'$__' -> 작은 따옴표 안에 문자 그냥 달러라는 문자

"$__" -> 큰 따옴표로 감싸야한다.

**특수변수**
- $0 : 실행파일
- $1 : 실행인자1
- $2 : 실행인자2
- $* : 실행인자 전체
- $# : 인자 개수
- $? : 바로직전에 수행한 명령 결과
  - 정상 : 0
  - 비정상 : 1 ~ 255
- $$ : 지금 수행중인 셸 PID
- ${변수명#pattern} :
- ##pattern : 패턴과 일치하는 부분을 앞에서 부터 찾아서 잘라버린다.
- %%pattern : 패턴과 일치하는 부분을 뒤에서 부터 찾아서 잘라버린다.

**변수선언**
- 변수=
- 변수=$(명령어   )
- 변수="$변수     "

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/40072aba-5401-49a5-85ed-d86a45b4a9ae)

---

#### case~esac문

```bash
#!/bin/sh
case $변수명 in
  pattern1)
    echo 명령어;;
  pattern2)
    echo 명령어2;;
esac
```

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/44885107-25de-43e3-99a6-49c67484ec4d)

### 반복문

#### for~in문
```bash
for 반복변수명 in 값1 값2
do
    명령어
      .
      .
done
```

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/bc5ac01f-51c3-4e9d-b7c0-ded052833779)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5fefaf1d-d7e7-45a0-a0fd-564368e25792)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/dd0b17db-d024-4ca4-a815-3342cfb9809c)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4377ec3f-7762-4735-9850-af98b4e0aa21)


#### 배열 사용하기

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/88e2547b-176f-4959-a3d3-0a5504bc5864)

#### While

```bash
#!/bin/bash
while [ 명령 ]
do
  명령
done
exit

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/8e064ba0-1812-4e9a-b8e1-9209cbb4aa52)




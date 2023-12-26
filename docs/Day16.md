# Day16(12월26일)

**continue** : 반복문의 다음 조건으로 넘어가게 한다.

**exit** : 해당 쉘 프로그램을 완젼히 종료한다.

**break** : 해당 반복문만 종료한다

### 함수

**선언**
```bash
함수명 () 
{

  return 
}
```

**호출**<br>
`함수명 [파라미터] [파마리터]`

**리턴값 처리**<br>
`변수=함수명`

### 함수연습
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4a8719bd-931b-4b22-a5a0-c367226a6f3f) ![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/510eb642-8f47-4ef8-a80d-acec63e099bf)

**다양하게 함수 활용하기**

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2864c523-75b5-46d2-8a87-5e888fcbd811)

**배열 활용하기**

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/53ba14ec-a826-4b00-9098-af1da528f991)

## 파일시스템

### 파일시스템 구성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/57bf68de-4ec6-4954-addb-3741ecf60311)

- ext3 -> ex2 + journaling 기능
- ext4 -> 대용량 파일시스템, 최대 16TB 파일시스템, 2TB 파일
- brfs -> b-tree 파일 시스템 Enterprise형 차세대 파일시스템, 최대 1EB 파일시스템 ,16TB 파일

#### 파일시스템 추가

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/cddde5a7-4ed8-4bf8-b7e8-48b87e23c27e)

- 파일시스템 포맷 - `mkfs`
  - ext3, ext4, xfs
- 파일 시스템 연결 - `mount`
  - mount 명령 또는 /etc/fstab


 ### LVM
**-> 여러개의 디스크를 합쳐서 1개의 파티션으로 구성한 후 다시 필요에 따라서 다시 나눠야 하는 상황에 주로 사용된다.**

- 물리 볼륨 : /dev/sda1, /dev/sdb1 등의 파티션을 말한다.
- 볼륨 그룹 : 물리 볼륨을 합쳐서 1개의 물리 그룹으로 만든 것이다.
- 논리 볼륨 : 볼륨 그룹을 1개 이상으로 나눈 것으로, 논리적 그룹이라고도 한다.

#### LVM 구성
- 파티션 타입 : linux LVM
- 물리적 볼륨 생성 : pvcreate
- 논리적 볼륨 그룹 생성 : lvcreate
- 볼륨확장 : vgextend / lvextend
- 파일시스템 용량 증설 : resize2fs(ext계열)/xfs_growfs(xfs)

### LVM구성하는법
- 디스크 추가
- `fdisk /dev/sda' 파티셔닝
- `pvcreate /dev/sda1` `pvcreate /dev/sda2`로 pv생성
  - `pvs`로 생성된 pv확인
- `vgcreate vg00 /dev/sda1 /dev/sda2`로 vg생성
  - `vgs`로 생성된 vg확인 
- `lvcreate -L 7G vg00 -n lv00`로 vg00에서 7G를 lv00에 할당 
  - `lvs`로 생성된 lv확인
- `mkfs.ext4 /dev/vg00/lv00`으로 lv00 ext4타입으로 포맷
- `lvextend -L +2G /dev/vg00/lv00`으로 2G 추가할당
- `mkdir`로 마운트 포인트 생성
- `vi /etc/fstab'에서 `UUID 마운트포인트 ext4 0 0 `추가
- `-mount -a`로 fatab에 있는 모든 파일시스템을 마운트한다.



  
 

 












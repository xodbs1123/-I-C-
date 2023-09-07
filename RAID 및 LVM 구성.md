### RAID 정의 및 개념 ###
- RAID
  - 여러 개의 디스크를 하나의 디스크처럼 사용
  - 비용 절감 + 신뢰성 향상 + 성능 향상
- 하드웨어 RAID
  - 하드웨어 제조업체에서 여러 개의 하드디스크를 가지고 장비를 만들어 그 자체를 공급
  - 안정적이지만 비쌈
- 소프트웨어 RAID
  - 고가의 하드웨어 RAID의 대안
  - 운영체제에서 지원하는 방식
  - 저렴한 비용, 안전하게 데이터 저장
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/e965485e-72eb-4da3-892a-3a730614b08c/image.png)

- RAID 1은
  - active + stanby 로 유지
- VMware 서버에 디스크 9개 추가

![](https://velog.velcdn.com/images/xodbs1123/post/13c12a55-9c28-4afa-9d58-a206a3c52eb9/image.png)

- fdisk를 통한 파티션 설정
- command : t > hex code는 디스크 타입 변경, fd는 레이어드 구성에 사용하는 파일 시스템

![](https://velog.velcdn.com/images/xodbs1123/post/88911081-c23b-4f05-961f-e283ce88d460/image.png)

### 레이드 구성 ###

- linear 레이드 구성도 (level=linear, 0, 1, 5 )

![](https://velog.velcdn.com/images/xodbs1123/post/7a7883ec-07cb-4b62-93c7-e9d725eee5ff/image.png)

- mdadm 명령어를 사용하여 sdb1과 sdc1을 linear raid로 묶는다

![](https://velog.velcdn.com/images/xodbs1123/post/f3aff043-513c-4bd6-8bee-232be655f3ae/image.png)

- 파일시스템으로 포맷 후 새로 생성한 디렉토리에 마운트!!

![](https://velog.velcdn.com/images/xodbs1123/post/cb67ef0c-059d-4a74-aa1a-d8c0cd2b2cdd/image.png)

- fstab을 활용하여 저장, 부팅후에도 유지될 수 있게!!

![](https://velog.velcdn.com/images/xodbs1123/post/7f293851-34a7-4fae-b2d6-711fe1838fac/image.png)


[참고하면 좋은 링크](https://itdexter.tistory.com/311)

### 레이드 복구 ###
- 고장난 하드디스크 교체

![](https://velog.velcdn.com/images/xodbs1123/post/eeaa1dce-8354-4a27-ba41-7424e9e7eb08/image.png)

- 교체한 하드디스크 파티션 재설정

![](https://velog.velcdn.com/images/xodbs1123/post/e1264eed-134e-4696-927f-f8213d0750eb/image.png)
- 마운트 해주기 전 RAID 작동 멈춘 후 마운트
- 완전히 제거된 RAID는 처음부터 다시 생성하면 되지만 RAID 1 or 5는 존재하고 있으므로 새로운 하드디스크만 추가해준다
- 예) mdadm /dev/md1 --add /dev/sdg1

![](https://velog.velcdn.com/images/xodbs1123/post/5d1afc61-ee49-4c45-874f-dc4624fe246f/image.png)



### LVM ( Logical Volume Manage ) ###
- 기능
  - 여러 개의 하드디스크를 합쳐 한 개의 파일시스템으로 사용
  - 상황에 따라 다시 나눌 수 있음
  - 2TB를 2개 합쳐서 4TB, 다시 1TB와 3TB로 나눌 수 있음
- 용어
  - Physical Volume : /dev/sda1, /dev/sdb1 등의 파티션
  - Volume Group : 물리 볼륨을 합쳐 1개의 물리 그룹으로 만드는 것
  - Logical Volume : 볼륨 그룹을 1개 이상으로 나누어 논리 그룹으로 나눈 것
 
 - 흐름도
 
 ![](https://velog.velcdn.com/images/xodbs1123/post/a8219270-ca46-47c5-986b-9c8b05068725/image.png)

- 디스크 2개 추가 (2GB, 3GB)
- 파티션 할당, 타입은 LVM 타입 ( Hex code : 8e )

![](https://velog.velcdn.com/images/xodbs1123/post/9fd50a5f-9403-408d-b3ef-be8f41c6b216/image.png)

- 물리 볼륨, 볼륨 그룹 생성

![](https://velog.velcdn.com/images/xodbs1123/post/b397af45-eb93-4541-a0b5-a6a940d0fdc6/image.png)

- 이후 논리 볼륨으로 용량 할당, 이후 포맷

![](https://velog.velcdn.com/images/xodbs1123/post/7f7c9425-be2d-4623-87a2-3f5f6d9bb82b/image.png)

- 디렉토리 생성 후 마운트하면 끝

![](https://velog.velcdn.com/images/xodbs1123/post/db07ea3f-3338-4a83-ac99-678f9d1b89db/image.png)

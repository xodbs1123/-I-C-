## Samba 서버 ##
- Windows와 Linux/Unix 사이 자원을 공유하기 위해 개발
- Linux에서 Windows의 자원 사용 방법과 Windows에서 Linux 자원을 사용하는 방법으로 나뉨
- 리눅스에서 Windows 폴더와 프린터 사용하기 위한 구성도

![](https://velog.velcdn.com/images/xodbs1123/post/a68ac395-4b49-44c0-8487-33cca2321c13/image.png)

## 윈도우 폴더를 리눅스에서 사용하기 ##
 - c드라이브에 smbshare 폴더 생성 후 공유 everyone 설정

![](https://velog.velcdn.com/images/xodbs1123/post/838485ce-c8d3-4ba5-903f-ace0db194c3c/image.png)

- cmd (관리자 권한) 에서 계정 생성

![](https://velog.velcdn.com/images/xodbs1123/post/a8a72c85-cf94-4d66-b8e3-38da6204c320/image.png)
- 본인 PC IP 확인
- 리눅스 서버에서 samba-client 설치 및 samba 설치 여부 확인

![](https://velog.velcdn.com/images/xodbs1123/post/55718ce1-d3e2-4c06-88ec-80f01ea88a1c/image.png)

- 리눅스에서 윈도우가 가지고 있는 공유 리스트 뭐 있는지 확인

![](https://velog.velcdn.com/images/xodbs1123/post/4f8690b2-202e-44cf-a9d3-0ac6a8a4c786/image.png)
- 윈도우 공유 파일과 리눅스 공유 파일을 연결하기 위해 디렉터리 생성 후 마운트

![](https://velog.velcdn.com/images/xodbs1123/post/e4ad000e-65d8-4bd9-a376-5d19e568778b/image.png)

- mount 된 모습

![](https://velog.velcdn.com/images/xodbs1123/post/c3ee1787-643b-4841-9e1c-5fc39501037f/image.png)

- 파일 공유 모습

![](https://velog.velcdn.com/images/xodbs1123/post/6b050e2c-03eb-4e9f-ba87-ea8afc06bb05/image.png)

![](https://velog.velcdn.com/images/xodbs1123/post/ddbff16b-6eb2-4af0-9d18-4e6c5ebb82db/image.png)


## Windows에서 리눅스 자원 사용하기 ##
- samba, samba-client 설치
- 공유 디렉터리 생성, 그룹 생성 (여러 공유 디렉터리를 만들 경우 편의성을 위해), share 디렉터리를 그룹의 소유로 변경, share 디렉터리 권한 부여, centos 계정을 sambagroup으로 이동 후 비밀번호 설정

![](https://velog.velcdn.com/images/xodbs1123/post/11b744d4-2611-449a-b1e3-ac15752b90e5/image.png)

- samba 파일 수정 및 공유 파일 내용 추가

![](https://velog.velcdn.com/images/xodbs1123/post/754c2ca4-9a73-4206-b546-e4167453b2ac/image.png)

- testparm 으로 파일 로드 확인

![](https://velog.velcdn.com/images/xodbs1123/post/4aa1b14b-1a42-4940-978e-0a299b9f88a9/image.png)

- smb nmb 재시작 및 활성화
- 방화벽 비활성화
- windows 내 PC > 네트워크 드라이브 연결

![](https://velog.velcdn.com/images/xodbs1123/post/49cc2866-5dad-444e-be87-96969dc12ea8/image.png)

- 로그인 후 공유 폴더 생성 된 모습

![](https://velog.velcdn.com/images/xodbs1123/post/81e15968-c40e-4701-8521-1a8f2443f896/image.png)

- 해당 폴더에 파일 넣어서 리눅스에서 확인 가능

![](https://velog.velcdn.com/images/xodbs1123/post/c1e0b1f2-a77c-437d-9827-dd0cf2e1b5de/image.png)

## Samba 서버 설정 파일 (smb.conf) ##
- /etc/samba/smb.conf 파일
  - [global] : 모든 자원들의 공유를 위한 설정
    - workgroup = Windows의 작업 그룹 이름
    - server string = Windows의 네트워크에 보이는 컴퓨터 이름
    - netbios name = Windows의 네트워크에 참가하는 컴퓨터 이름
    - hosts allow = Samba 서버에 접속을 허용할 컴퓨터의 IP 주소
    - log file = Samba 서버에 접속하는 컴퓨터의 접속 기록 파일
    - securit = usre(CentOS 8에 포함된 버전은 share을 허용하지 않음)
  - [공유이름] : 공유되는 디렉토리에 대한 설정
    - comment = 공유하는 디렉터리를 설명. 생략 가능
    - path = 물리적인 디렉터리
    - read only = 디렉터리에 쓰기 권한이 있는지 여부. yes는 읽기 전
	  용, no는 읽기/쓰기 허용
    - browseable = 공유 리스트를 보여줄지 여부
    - guest ok = 다른 사용자도 사용하게 할지 여부

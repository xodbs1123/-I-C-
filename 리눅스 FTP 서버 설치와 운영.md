## FTP ##
- 파일을 전송하기 위한 서비스
- 파일 전송 자체를 위해서는 성능이 뛰어남
- vsftpd는 CentOS에서 제공해줌 ( 리눅스와 유닉스 환경에서 보안성과 성능이 우수한 FTP 서버 )
## Vsftpd 설치 ##
 - dnf -y install vsftpd
 - vmlinuz-4로 시작하는 파일을 file1으로 합침

 ![](https://velog.velcdn.com/images/xodbs1123/post/1d69e569-229b-434b-bd5f-38f037db24f4/image.png)

- /etc/vsftpd/vsftpd.conf 수정 ( 익명=게스트 접속 허용 )

![](https://velog.velcdn.com/images/xodbs1123/post/9e9ca1d1-8327-4b3a-8e30-dc19fcb00ed1/image.png)
- FileZilla Client (인터넷 검색) 기본 다운 및 설치
- FileZilla 세팅

![](https://velog.velcdn.com/images/xodbs1123/post/6cd65ec8-f887-45ad-8fcc-cc6ebaf7e267/image.png)

- 리눅스 서버와 연결되어 pub 파일이 생성된 모습

![](https://velog.velcdn.com/images/xodbs1123/post/134d22e2-c3af-46c4-bd72-4b68d320593c/image.png)

- 리눅스 서버에 있는 파일을 다운로드 받을 수 있음
- 윈도우 파일을 리눅스 서버 디렉토리에 넣기 위해 /etc/vsftpd/vsftpd.conf 수정

![](https://velog.velcdn.com/images/xodbs1123/post/1076daf8-f74e-4882-9fd1-e5a18d0ecc15/image.png)

- pub 폴더의 소유를 root가 아닌 ftp가 할 수 있도록 권한 변경

![](https://velog.velcdn.com/images/xodbs1123/post/20714e7c-2c32-42e8-b2f5-202a1dc20818/image.png)

- 새로운 사이트 추가 세팅

![](https://velog.velcdn.com/images/xodbs1123/post/8c1bc9bf-a06d-4a50-9bc0-a3e831df718d/image.png)

- 이후 정상적으로 윈도우 파일을 리눅스 서버로 업로드 가능

## Vsftpd.conf 옵션 ##
- anonymous_enable : anonymous(익명) 사용자의 접속을 허가할지 설정
- local_enable : 로컬 사용자의 접속 허가 여부 설정
- write_enable : 로컬 사용자가 저장, 삭제, 디렉터리 생성 등의 명령을 실행하게 할 것인지 설정 (anonymous 사용자는 해당 x)
- anon_upload_enable : anonymous 사용자의 파일 업로드 허가 여부를 설정
- anon_mkdir_write_eanble : anonymous 사용자의 디렉터리 생성 허가 여부를 설정
- dirlist_enable : 접속한 디렉터리의 파일 리스트를 보여줄지 설정
- download_enable : 다운로드 허가 여부 설정
- listen_port : FTP 서비스의 포트 번호를 설정 ( 기본 : 21 )

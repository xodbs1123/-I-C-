## PXE 서버 ##
- 개념도

![](https://velog.velcdn.com/images/xodbs1123/post/5ff9b3c1-fe52-4f74-bed2-ea52c6e867fc/image.png)

- syslinux, dhcp-server, tftp-server, vsftpd 설치
  - dnf -y install syslinux dhcp-server tftp-server vsftpd
- 방화벽 비활성화
- dhcpd.conf 파일, vsftpd.conf 파일 수정

![](https://velog.velcdn.com/images/xodbs1123/post/21762621-9363-4459-ab96-aeabc0bc37f9/image.png)

- cd umount 후 다시 마운트 해준다

![](https://velog.velcdn.com/images/xodbs1123/post/1382ca3a-09b5-4e88-a69a-33e9291c4ba8/image.png)

- cd에 있는 내용을 복사해서 tftpboot에 넣는다 + pxelinux

![](https://velog.velcdn.com/images/xodbs1123/post/00b73701-a07b-4745-bfe6-aee882c8a077/image.png)

- pxelinux.cfg 디렉터리 생성 후 default 파일 생성 및 CentOS8 자동설치를 위한 내용 입력

![](https://velog.velcdn.com/images/xodbs1123/post/b027f642-6d6e-4f2e-8306-1b1d94f3b53e/image.png)

- syslinux, dhcp-server, tftp-server, vsftpd 재시작
- 새로운 서버 만들고 ( CD 없이 ) 실행하면 자동 설치 됨

![](https://velog.velcdn.com/images/xodbs1123/post/78ee93fa-0786-40e0-82c6-dc25107560a0/image.png)

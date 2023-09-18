## DHCP ##
- DHCP ( Dynamic Host Configuration Protocol )
  - 자신의 네트워크 안에 있는 클라이언트 컴퓨터가 부팅될 때 자동으로 IP주소, 서브넷 마스크, 게이트웨이 주소, DNS 서버 주소를 할당해 주는 것
  
- 일반 사용자가 IP에 관련하여 정보를 몰라도 인터넷 사용하는 데 문제가 없는 이유
- 관리가 편하고 이용자가 편함
- 한정된 IP 주소로 여러 명의 사용자가 사용할 수 있음
- 작동 원리

![](https://velog.velcdn.com/images/xodbs1123/post/d5ef635f-b9d6-41f6-8797-4cd29e7047d9/image.png)

- VMware에서 DHCP 서버 구성도

![](https://velog.velcdn.com/images/xodbs1123/post/af77c5df-9181-4e25-80ca-157bb972ae88/image.png)

- rpm -qa dhcp-client로 설치 확인 ( client, server(b) )
- Vm pro DHCP 서비스 해지

![](https://velog.velcdn.com/images/xodbs1123/post/ba997343-d59c-431f-86f5-c6b272b43097/image.png)

- client IP 못받아오는 모습

![](https://velog.velcdn.com/images/xodbs1123/post/cb83fab7-38e0-4c7d-9b6d-050fedd55772/image.png)
- server(b) 세팅
  - BOOTPROTO = dhcp
  - IPaddress ~ DNS1까지 삭제
  - reboot
  
  ![](https://velog.velcdn.com/images/xodbs1123/post/a6275ccb-def9-4e63-871b-09f4889894a0/image.png)

- server에 dhcp-server 설치 ( dnf -y install dhcp-server )
- /etc/dhcp/dhcpd.conf 에서 DHCP 세팅 

![](https://velog.velcdn.com/images/xodbs1123/post/04edee1f-abe3-421e-8ca8-52c045b171e5/image.png)

- dhcpd 디렉토리에 있는 파일 확인 ( DHCP에 쓰이는 IP 리스트 작성 )

![](https://velog.velcdn.com/images/xodbs1123/post/aa906c42-686f-4cc1-8f04-5c734321dd4d/image.png)
- dhcpd 재시작후 활성화 ( systemctl restart/enable dhcpd )
- server(b)와 client 재부팅하면 정상적으로 IP 받아옴

![](https://velog.velcdn.com/images/xodbs1123/post/94b09e66-14c3-4639-b944-c7cf923ea17e/image.png)

![](https://velog.velcdn.com/images/xodbs1123/post/6514249c-a431-4368-83f1-ac0206711507/image.png)

- dhcpd.lease 파일에서 접속중인 IP 확인할 수 있음

![](https://velog.velcdn.com/images/xodbs1123/post/7278a7f5-0d1d-4beb-a190-a77363b12d42/image.png)

## /etc/dhcpd.conf 내용 ##

![](https://velog.velcdn.com/images/xodbs1123/post/88461a25-f15e-4752-97a9-9e95781577e0/image.png)

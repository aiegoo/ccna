NAT 

inside local address 를 inside global address 로 변환
=>내부의 ip 를 외부의 ip 로 변환
=>내부의 사설 ip 를 외부의 공인 ip 로 변환
=>보안성이 좋아진다. ip 고갈문제를 해결

inside local를 outside global로 translate 해줌

1:35 PM  video recorded 녹화 끝 - nat 개념


정보 확인

sh ip nat translations  : NAT table 정보 확인
sh ip nat statistics : NAT 가 동작하는 통계치
debug ip nat            : NAT 주소 변환 정보 debug

clear ip nat translations *  : 생성된 NAT table 삭제


1>NAT 설정 


-static  :  1:1  지정 방식 

ip nat inside source static 10.1.1.1  172.16.1.1


int s 1/0
ip nat outside

int f 0/0
ip nat insides


1:41 PM 녹화했음
-dynamic


  -pool 을 이용하는 방법

`access-list 10 permit ho 10.1.1.1
ip nat pool AAA 172.16.1.1 172.16.1.1 prefix-length 24
ip nat inside source list 10 pool AAA overload`


int s 1/0
ip nat outside

int f 0/0
ip nat insides


  -pool 을 이용하지 않는 방법

access-list 10 permit ho 10.1.1.1
ip nat inside source list 10 int s 1/0 overload

int s 1/0
ip nat outside

int f 0/0
ip nat insides


[참고]
설정을 할때에 필요한 내용
1>local address  필요
2>global address 필요
3>local address 를 global address 로 변환


2:04 PM
2>NAT 이론


-static  :  1:1  지정 방식 (설정을 하면 자동적으로 NAT table 이 생성이 되고 삭제(clear ip nat tr *)가 불가능하고 유지시간도 없다)
          

-dynamic :한번 변환이 되어야 NAT table 이 생성이 되고 삭제(clear ip nat tr *)가 가능하고 유지시간이 있다

  -NAT:단순 변환 , 1:1 방식 , 유지 시간 1일
  -PAT: 확장 변환,  1:다수 방식 , 유지 시간 1분 (overload)

2:21 PM  녹화 끝 nat pat 설정관련 개념



2:22 PM
DHCP

자동 ip 할당

ip 할당
(ip , subnetmask , default gatewqy , DNS 등등)
수동적으로 설정하는것은 매우 불편

그래서 자동 ip 할당을 하자  => DHCP


UDP

Server 가 67 번 포트를 사용   S ------------> C
Client 가 68 번 포트를 사용   C ------------> S


DHCP 동작  (기본 : broadcast )


DISCOVER : Client가 Server 에게 ip를 요청(client의 MAC주소 포함) Server 가 중복확인(unicast[ICMP]) broadcast

OFFER : Server 가 Client 에게 ip 를 할당 (client의 MAC이 목적지) broadcast

REQUEST :ip 사용에 대한 최종확인(client의 MAC포함) => DHCP 서버가 2대이상일수 있어서

ACK : 선택되지 않은 Server 는 ip를 회수 
     선택된 server는 나머지 정보(subnetmask,default gateway,DNS 정보등등)를 할당 승인 broadcast

 출발지 ip        목적지 ip		
Client     68 번 포트를 사용   C ------------> S     DISCOVER        0.0.0.0        255.255.255.255
Server    67 번 포트를 사용   S ------------> C     OFFER            Server ' ip     255.255.255.255
Client     68 번 포트를 사용   C ------------> S     REQUEST         0.0.0.0        255.255.255.255
Server    67 번 포트를 사용   S ------------> C     ACK               Server ' ip     255.255.255.255

2:33 PM

할당할 네트워크 : 192.168.1.0  /24 
기본 게이트웨이 : 192.168.1.254 
DNS 서버 : 192.168.1.252  , 192.168.1.253
도메인 name : voice.com
임대 기간 : 무제한 
내부에서 사용중인 서버 : FTP서버 (192.168.1.250) , WEB서버(192.168.1.251) ,Mail서버(192.168.1.100)

ip dhcp excluded-address 192.168.1.100
ip dhcp excluded-address 192.168.1.250 192.168.1.254

ip dhcp pool AAA
network 192.168.1.0 /24
de
default-router 192.168.1.254
dn
dns-server 192.168.1.252 192.168.1.253
do 
domain-name 
l
lease infinite

do sh run | s dhcp
do sh int bri

[참고]
'ip helper-address' 기능

-수신한 브로드케스트를 유니케스트로 변환시켜주는 기능

ip forward-protocol udp[port #]  
--- end 2:46 PM

2:49 PM
연습문제  
https://cafe.naver.com/itguild/645

3:30 PM 3:39pm 동영상

라우팅

routing 

router 가 ip 헤더안에 있는 목적지 ip를 보고 routing table 을 참조해서 
목적지가 있는 방향쪽 interface 로 packet 전송

Switch 는  switching

switching 

Switch 가 Ethernet  헤더안에 있는 목적지 mac주소를 보고  mac-address table 을 참조해서 
목적지가 있는 방향쪽 port 로 frame 전송


mac address table 을 참조
=>  mac address table 에 있어야만 제대로 전송이 가능 
      mac address table 에 없어도 전송이 가능 (flooding)

=> 기본적으로mac address table 이 없다 =>mac address table 을 완성
=>switch가 알아서 완성 (TransParent Bridging)


Transparent Bridging


-Learning : Mac address 를 학습하는 상태
 수신한 정보의 출발지 mac address 가 switch 의 mac address table 에 없는 정보면          
 switch 가 알아서 학습 한다

-Flooding : 수신한 port 를 제외한 나머지 port 에게  전송

(플러딩을 하는 경우)
1>broadcast 를 수신하는 경우 broadcast 로 플러딩
2>unknown unicast를 수신하는 경우 unicast로 플러딩
3>unknown multicast 를 수신하는 경우 multicast로 플러딩    

[참고]
unknown : 목적지 mac 주소가 mac address table 에 없는 주소(정보)


-Forwarding :mac address table 참조해서 전송

-Aging : mac address table 유지 시간 300 초(5분) =>사용되지 않는 정보가 먼저 삭제가 된다


-filtering :정보를 수신한 port 와 목적지port 가 동일하면 정보를 전송하지 않는다


Network 장비

L1 : Hub -전기적인 신호를 증폭 ,같은 CD(충돌영역)안에 있다,Half-duplex

L2 : Switch - CD(충돌영역)을 나누어 준다 ,full-duplex,  BD(broadcast domain)안에 있다
 
L3 : Router - 물리적으로 BD(broadcast domain)을 나누어 준다


VLAN(Virtual Local Area Network)


논리적으로 broadcast domain 을 나누어 준다

-broadcast traffic 의 영향을 최소화 시켜준다
-broadcast 로 인한 LAN 구간 성능저하를 최소화 
-ARP broadcast차단으로 unicast 접속이 불가능(보안) 
=>장비 소모량이 줄어든다 

A  vlan  =  A logical Network  =  A subnet  =  A  broadcast domain


vlan 범위

1 ~ 4094


vlan 종류


standard (vlan 1,1002,1003,1004,1005 ): 기본 생성이 되어 있고 수정 및 삭제가 불가능)

1 ~ 1005

[참고]
모든 port 는 기본적으로 vlan 1 에 속해있다
기본적으로 지원되는 최대 vlan  갯수는 1005개 

[참고]
VTP 서버 모드는 Standard VLAN 1~1005까지만 생성 및 관리가 가능하다

extended

1006 ~ 4094

[참고]
VTP transparent 모드는 extended  생성 및 관리가 가능하다


[vlan 구성 방법]

1.vlan 생성 ,수정 ,삭제 (sh vlan bri)


vlan 11       생성
name HR     수정

no vlan 11   삭제

vlan 11-20 : vlan 11 ~ 20 까지 한번에 생성

no vlan 2-1001 : vlan 2 ~ 1001 까지 한번에 삭제

 
Vlan 은 NVRAM 에 저장되지 않고  flash memory 안에 vlan.dat 라는 파일로 저장이된다 
그래서 vlan은 reload 로 삭제되지 않는다 
그래서  vlan을 삭제하려면 vlan.dat 파일을  delete flash:vlan.dat 명령어로 삭제하고 reload ~


2.해당 port 를 해당 vlan 에 매핑(access)  sh vlan bri

int f 0/1
switchport mode access
switchport access vlan 11

int r f0/1-5,f0/7-9
sw m a
sw a v 11


4:40pm


3.trunk 완성  sh int tru

DATA에 vlan-id(vlan번호)를 tagging 해주는것


int f 0/24
switchport trunk encapsulation ?

isl       : cisco           Native vlan X
dot1q : IEEE 802.1q  Native vlan O


Native vlan : DATA 에 vlan-id 가 없는 경우에 처리되는 vlan 으로 기본값 vlan 1  
 변경할수 있고 switch 간의 native vlan 이 동일해야 한다



int f 0/24
switchport trunk encapsulation dot1q
switchport mode trunk


int r f 0/22-24
sw t e d
sw m t


trunk 옵션 


allowed : vlan 허용 범위

int f 0/24
switchport trunk allowed vlan 11-20

vlan 11 ~ 20 까지만 trunk 허용

기본은 1 - 4094


native : native vlan 지정

int f 0/24
switchport trunk native vlan 10

native vlan 을 10으로 지정

[주의] switch 간의 native vlan 이 동일해야 한다


[참고]

dot1q 만 지원되는 스위치 

int f 0/24
switchport mode trunk


5:17 PM
4.VTP(Vlan Trunk Protocol) sh vtp status

vlan database 정보를 trunk port 를 통해서만 교환하는 protocol
(옵션:설정을 한다면 가장 먼저 설정하는것이 좋다: vlan 구성 용이,vlan 관리 용이,trunk설정 완성을 확인)

5:24 PM
VTP 구성 조건


-vtp domain 일치(필수):trunk 설정이 완성되어있다는 전제하에 하나의 switch 에서 
vtp domain 설정을 하면  나머지 switch 에서 vtp domain을 공유 한다

설정 : vtp domain CISCO

-vtp password(옵션):최소한의 인증,password가 다르면 공유를 하지 않음
 sh vtp pass

설정 : vtp pass cisco

-trunk 완성 



[vtp mode]

Server:vlan 생성,수정,삭제   가능,일치 O ,중계 O
Client:vlan 생성,수정,삭제 불가능,일치 O ,중계 O

Transparent:vlan 생성,수정,삭제 가능,일치 X , 중계 O


5:27 PM
[vtp mode]

Server:vlan 생성,수정,삭제   가능,일치 O ,중계 O
Client:vlan 생성,수정,삭제 불가능,일치 O ,중계 O

Transparent:vlan 생성,수정,삭제 가능,일치 X , 중계 O


기본 mode 는 Server

설정

vtp mode server
vtp mode client
vtp mode transparent


5:34 PM


12:51 PM
Day8

연습문제 네이버 까페
https://cafe.naver.com/itguild/646


5. inter-vlan

서로 다른vlan 을 통신 시켜주기 위해서 L3(Router)장비에서 설정해주는 vlan routing 이다

=>각각의 vlan 에 대해서 default gateway 를 구성 


[참고]
물리적인 interface의 고갈을 해결하는 방법
=> subinterface 를 구성

subinterface :물리적인 interface 토대위에 만들어준논리적인 interface 

R1

int f 0/0
no shut

int f 0/0.11
encapsulation dot1q 11
ip add 192.168.11.254 255.255.255.0

int f 0/0.12
en d 12
ip add 192.168.12.254 255.255.255.0

int f 0/0.13
en d 13
ip add 192.168.13.254 255.255.255.0



[참고]
스위치는 MAC 주소 기반으로 프레임을 전송하기 때문에 스위치 포트에 IP 주소 설정이 불필요하다
스위치를 관리하기 위해서 텔넷 접속을 하거나, 또는 스위치 Ping 테스트, Cisco IOS 다운로드/업로드를 하기 위해서는 IP 주소가 필요하다. vlan 에 ip 를 설정해준다 

vlan 1 은 기본 생성이 되어있고 모든 port는 기본적으로 vlan 1 에 속해있고 native vlan 도 기본적으로  vlan 1 이기때문에 vlan 1 에 설정하는것이 가장 효율적이다 


int vlan 1
ip add 1.1.1.1 255.255.255.0
no shut


1:47 PM

Network 구축의 핵심

-확장성
-이중화
-백업
-로드 분산


Router 간의 이중화는 문제가 없다
 
Switch 간의 이중화는 문제가 발생 (bridging Loop : 브릿징 루프)가 발생


 Bridging Loop 종류
 -broadcast storm
 -copy unicast frame (유니케스트 프레임을 복제) 1:54 PM vedeo recorded
 -MAC Flapping (MAC 주소 테이블 불안정화)



2:06 PM

STP spanning tree protocol
스위치간의 물리적으로 이중화 되어 있는 구간을 논리적으로 block 시켜주는 것
=> siwtch 간의 이중화 구현이 가능 하다
=> 이중화 구간이 X 개면 block 도 X 개여야 한다
1:43 PM video recorded


STP 종류

802.1d  STP (PVST)       0
802.1s  MSTP              3
802.1w RSTP               2 


port 유형

-DP(지정  port) : 설정 BPDU 를 송신  or  TCN BPDU 를 수신 
-RP(Root port) : 설정 BPDU 를 수신  or  TCN BPDU 를 송신
-AP(대체  port) : 설정 BPDU 를 수신만 한다 , 논리적으로 block 



port 상태

-disable : shutdown 상태, 혹은 cable 이 연결이 안된 상태 , BPDU gurad or port-security 로 인한
              shutdown  상태 , DATA 송수신 불가능 , BPDU 송수신도 불가능 

-blocking : 논리적으로 block 된 상태(bridging loop 를 방지) ,BPDU 를 수신만 한다, max-age 20 초
                 => max-age동안 BPDU 를 수신못하는 경우 , 후순위 BPDU를 수신한 경우

-listening : port 역활(유형)을 지정 (DP,RP,AP 지정)   ,forward-delay :15 초 

-learning : mac-address 를 학습하는 상태   ,forward-delay :15 초 

-forwarding : DATA 송수신이 가능한 상태 
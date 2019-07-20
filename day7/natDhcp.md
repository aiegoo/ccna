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

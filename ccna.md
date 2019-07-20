1.지각, 결석 X
2.복습하기 
3.대답하기 

+필기하기 X

cafe.naver.com/itguild         네트워크 기초
cafe.naver.com/itwillcisco    네트워크 중급 및 네트워크 보안 



Protocol  :  언어  ,  약속 



장비 구성 방법

-TUI : 툴기반
-GUI : 경로 (그래픽) 
-CLI : 설정 (커맨드) -필수 설정  : 설정을 하지 않으면 통신이 안되는 설정
                -옵션  설정 : 설정을 하지 않아도 통신이 되는 설정  => 해주면 좋아~ 




Network

연결 
-정보의 공유 (정보 : 컴퓨터 관점에서는 DATA라고 한다)
-DATA 는 전기적인 신호로 변환 되서 통신이 된다 
전기적인 신호 단위 : bit

참고> DATA 를 저장 : byte , DATA 를 전송 :bit
+ 1byte = 8 bit


Network 종류

LAN(Local Area Network)
사용자가 포함된 비교적 좁은 지역의 소규모 네트워크 
비용 : 초기-많다    유지-적다 
관리 : 내부 관리자 
속도 : 100baseTx


100 : 100M

base : 디지털
+broad : 아날로그



Tx : TP

4TP : 8 가닥


TP 구조

1  화주
2     주
3  화초
4     파
5  화파
6     초
7  화빨
8     빨


TP 종류

UTP : EMI( 전자 간섭 ) 의 영향을 받는다 
STP : EMI( 전자 간섭 ) 의 영향을 받지 않는다 => 속도가 빨라진다



UTP 종류

-관리 목적 : Rollover ,Rolled , 콘솔 케이블 , 관리자 케이블 


1 8
2 7
3 6
4 5
5 4
6 3
7 2
8 1


-통신 목적 

  - 다른 장비 : 다이렉트


1 1
2 2
3 3
4 4
5 5
6 6
7 7
8 8

  - 같은 장비 : 크로스 오버

 
1,3,2,6 을 서로 교차

1 3
2 6
3 1
4 4
5 5
6 2
7 7
8 8


장비  : Switch  ,Hub


WAN(Wide Area Network)
LAN 과 LAN 들을 연결시켜주는 광역 네트워크 , 주로 ISP 업체 이용
비용 : 지속적으로 든다 
관리 : ISP 업체 
참고> T1 (1544k) E1(2048k)  1M = 1000k
장비: Router 
Router: 네트워크를 연결시켜주거나 분활/구분 시켜주는 장비




Network 구축의 핵심

-확장성
-이중화
  -백업
  -로드 분산



DATA 전송 관계

Server :Client가 요청을 하면 요청을 한 정보를 생성해서 주는

Client : Server 에게 요청을 한 정보를 받는 => 사용자에게 서비스 하는 ex> PC




IPv4 의 DATA 전송 유형

               DATA 수      client 수
unicast           1       :        1
broadcast       1       :    불특정 다수    
multicast        1       :    특정 다수


[참고]
broadcast 로 인한 LAN 구간 성능 저하를 가져올수도 있다 => 해결 방안 : VLAN



OSI 7 계층 참조 모델

컴퓨터 응용 프로그램 정보가 다른 컴퓨터 응용프로그램으로 어떤 과정을 통해서 이동하는지 설명

-네트워크 설계을 위한 기준을 제공
=>호환성 제공
=>T/S 용이


ex> 통신이 안되면 ping 명령어를 사용한다

ping 을 사용하면 
-ping 이 되는 경우     : L1 ~ L3 까지 문제 없다
-ping 이 안되는 경우  : L1 ~ L3 에서 문제가 있다 

이유는 ping 명령어는 ICMP protocol 을 사용한다
근데 ICMP 는 3계층 프로토콜이다 
+하위계층이 up이 되지 않으면 상위계층은 up 이 되지 않는다


상위계층 : DATA 를 생성  , 주로 OS 에서 담당 

7  어플리케이션 : 사용자를 위한 계층 
6  프레젠테이션 : 장비간의 커뮤니케이션
5  세션 : OS 간의 논리적인 연결(다양한 옵션 결정)   =>  PDU

하위계층 :DATA 를 전송(주소:출발지(Source) 목적지(Destination))

4 Transport[TCP or UDP][DATA]segment,port(16bit),0~65535(0~1023:well-known)S:랜덤 D:서비스타입

3 Network[IP][TCP or UDP][DATA]packet,,IPv4,32bit,10진수,논리적인 주소(설정 및 변경이 가능),Router

2 Data-link[Ethernet]][IP][TCP or UDP][DATA]frame,MAC주소,16진수,48bit(구조 체계:앞에 24bit 와 뒤에24bit로 구분되고 앞에 24bit 는 명칭이 OUI-24 라고 해서 회사 번호이고 뒤에 24bit 는 고유 번호)
물리적인 주소 => 이미 설정이 되어있고 변경이 불가능,실제 host 주소 , Switch

1 피지컬 : 전기적인 신호로 변환 및 출력 , HUB


L4 encapsulation protocol 

-TCP  :  연결 지향 서비스 (연결형 프로토콜)  => 3 way handshaking
신뢰적인 서비스 => Flow Control(흐름제어),error control & error correction(오류 제어 및 오류 정정)
Congestion Control (혼잡 제어)

-UDP :  비 연결 지향 서비스(비 연결형 프로토콜) , 비 신뢰적인 서비스 (Best Effort:BE방식)


L3 encapsulation protocol

-IP          : Best Effort 방식
-ICMP     :  Request(Type-8) => Reply(Type-0)(ping 을 이용)
-IGMP     :  multicast 확인용
-ARP       :  ip 를 이용해서 mac 주소를 알아온다


L2 encapsulation protocol

-LAN   : Ethernet  
-WAN : HDLC , PPP ,Frame-relay




Network 

L1 Hub      :  전기적인 신호를 증폭 , 같은 CD (충돌 영역) 안에 있다 , half-duplex , CSMA/CD
L2 Switch   :  CD(충돌 영역)을 나눠준다 , full-duplex , 같은 BD(broadcast domain) 안에 있다
L3 Router   :  물리적으로 BD(broadcast domain) 을 나눠준다


Ethernet 의 DATA 의 전송 유형

-half duplex  :  반 양방향      , 무전기
-full  duplex  :  완전 양방향  ,  전화기



Routing 

Router가 IP 헤더안에 있는 목적지 ip를 보고 routing table 을 참조해서 목적지 방향쪽 interface 로 Packet  을 전송 

+ 목적지까지 책임을 지는것이 아니라 다음 Router 까지만 책임을 진다

routing table 을 참조
1>routing table 에 정보가 있으면 전송이 가능
    routing table 에 정보가 없으면 전송이 불가능

목적지까지 책임을 지는것이 아니라 다음 Router 까지만 책임을 진다
=> 모든 router 가 모든 network 정보를 가지고 있어야 한다




ICMP

!!!!!  (핑이 된다 , 통신이 된다)

R1#ping 192.168.3.3

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.3.3, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 2/4/8 ms

..... (핑이 안된다 , 통신이 안된다) : Routing table 에 없을때 , Routing table 에는 있으나 목적지ip가 없을때,Request 는  도착했으나 reply 는 받지 못했을 경우 등등 

R1#ping 192.168.3.4

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.3.4, timeout is 2 seconds:
.....
Success rate is 0 percent (0/5)

UUUUU (핑이 안된다 , 통신이 안된다): routing table 에 정보가 있어서 출발은  했으나 목적지에 도달 못한 경우

R1#ping 121.160.70.2

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 121.160.70.2, timeout is 2 seconds:
U.U.U
Success rate is 0 percent (0/5)
                        


IPv4  32bit   10진수

구조 체계

8bit 씩 4개의 옥텟 

11111111.11111111.11111111.11111111

128    64   32   16   8   4   2   1
 

위의 숫자를 대입을 해서 bit가 들어가 있는 자리의 숫자들끼리 서로 더해준다 

255.255.255.255


128    64   32   16   8   4   2   1

172.16.8.1


10101100.00010000.00001000.00000001

172.16.8.1

128    64   32   16   8   4   2   1

10101010.01010101.00001111.11110000

170.85.15.240


11111000   248

11111100   252




subnetmask   

ip 를 규정 (network-id 와 host-id를 구분)
=>  host-id bit 가 전부 0 이면 network-name
=>  host-id bit 가 전부 1 이면 broadcast
=>  network-name 과 broadcast 는 둘다 사용을 못함 



=>/24  =>  prefix

11111111.11111111.11111111.00000000   =>  255.255.255.0 (subnetmask)

/27 => 255.255.255.224

/30 =>  255.255.255.252

/15  =>  255.254.0.0



172.16.1.254  /24
 

10101100.00010000.00000001.11111110
11111111.11111111.11111111.00000000 
10101100.00010000.00000001.00000000 

172.16.1.0 ~ 255 ( 1 ~ 254 )  /24


사용할수 있는 최대 host 수 ?  2^host-id-bit - 2  


172.16.1.32  /24

172.16.1.  00000000       0
~~~~~~~~~~~~~     ~~~ (1~254)  /24
172.16.1.  11111111     255


172.16.1.32  /27

172.16.1.001   00000     32
~~~~~~~~~~~~~~    ~~(33~62)   /27
172.16.1.001   11111     63



172.16.1.15  /27

172.16.1.000  00000       0
~~~~~~~~~~~~~~   ~~~(1~30)   /27
172.16.1.000  11111      31


172.16.1.123  /27

172.16.1.011   00000       96
~~~~~~~~~~~~~~     ~~~ (97~126)  /27
172.16.1.011   11111      127


(숙제) 네트워크 ID 와 호스트 ID 구분 및 범위 구하기



200.200.200.200  /28

200.200.200.1100    0000        192     
~~~~~~~~~~~~~~~~~        ~~~ (193~206)  /28
200.200.200.1100    1111        207 


200.200.200.200  /30

200.200.200.110010   00       200
~~~~~~~~~~~~~~~~~      ~~~(201.202)  /30
200.200.200.110010   11       203


---------------------------------------------------------------------------------------------

[참고]
/30  은  ip 가 딱 2개만 나오기 때문에  WAN Point-to-Point 구간에서 가장 효율적인 subnetmask 다

+동일한 network는 동일한 network-id를 가지고 서로 다른 network 는 서로 다른 network-id를 가진다

+network-id 가 5개면 network 가 5개인거고 network 가 5개면 routing table 이 5개씩 나와야 한다


IPv4   32bit   약 43억개 

class 

unicast  

A   0.0.0.0 ~ 127.255.255.255 (1.0.0.0 ~ 126.255.255.255)   /8
B   128.0.0.0 ~ 191.255.255.255                                     /16
C   192.0.0.0 ~ 223.255.255.255                                     /24

D   224.0.0.0 ~ 239.255.255.255   multicast  주소 
E    240.0.0.0 ~ 255.255.255.255   future  use 


classful 
subnetmask 를 무시 =>  default  subnetmask 를 사용

classless 
subnetmask 를 인정 

공인 ip (Public ip)
공중 네트워크 망을 사용할수 있는 ip , internet 을 사용할수 있는 ip , 주로 ISP 업체한테 임대해서 사용

사설 ip (Private ip)
공중 네트워크 망을 사용할수 없는 ip , internet 을 사용할수 없는 ip , 사설 ip 로 지정된 ip를 사용하기를 권장 

사설 ip

10.0.0.0  ~ 10.255.255.255
172.16.0.0  ~ 172.31.255.255
192.168.0.0  ~ 192.168.255.255

10.0.0.0        /8
172.16.0.0    /12    =  172.16.0.0  /16  ~ 172.31.0.0  /16
192.168.0.0   /16




subnetmask : ip 를 규정 (network-id 와 host-id를 구분)
subnet : subneting 이 된 network 
subneting : ip 의 낭비를 막기 위해서 원본 네트워크를 잘라주는것



192.168.100.0   /24   host = 25    2^x -2 >=25     x= 5


                2^3=8  2^5-2 =30
192.168.100.000  00000
255.255.255.111  00000     /27
192.168.100.000  0  ~31  (1~30)
192.168.100.001  32 ~63  (33~62)
192.168.100.010  64 ~95  (65~94)
192.168.100.011  96 ~127(97~126)
192.168.100.100  128~159(129~158)
192.168.100.101  160~191(161~190)
192.168.100.110  192~223(193~222)
192.168.100.111  224~255(225~254)


192.168.100.32 /27

192.168.100.001   00000            32
~~~~~~~~~~~~~~~~~         ~~~ (33~62)  /27
192.168.100.001   11111            63



VLSM

-ip 의 낭비를 막기 위해서 subneting 된것을 다시 subneting 해주는 것

host = 2   2^x-2>=2    x = 2

192.168.100.000  000  00
255.255.255.111  111  00       /30    
192.168.100.100  000  128~131(129.130)
192.168.100.100  001  132~135(133.134)
192.168.100.100  010  136~139(137.138)
192.168.100.100  011  140~143(141.142) 
192.168.100.100  100  144~147(145.146)
192.168.100.100  101  148~151(149.150)
192.168.100.100  110  152~155(153.154)
192.168.100.100  111  156~159(157.158)


192.168.100.153  /30


192.168.100.100110   00        152
~~~~~~~~~~~~~~~~~       ~~~(153.154) /30
192.168.100.100110   11         155




요약 

Routing table 의 크기를 줄여주기 위해서


Routing 

Router가 IP 헤더안에 있는 목적지 ip를 보고 routing table 을 참조해서 목적지 방향쪽 interface 로 Packet  을 전송 

+ 목적지까지 책임을 지는것이 아니라 다음 Router 까지만 책임을 진다

routing table 을 참조
1>routing table 에 정보가 있으면 전송이 가능
    routing table 에 정보가 없으면 전송이 불가능

목적지까지 책임을 지는것이 아니라 다음 Router 까지만 책임을 진다
=> 모든 router 가 모든 network 정보를 가지고 있어야 한다

그러므로 routing table 의 크기는 커질수 밖에 없다



그래서 routing table 의 크기를 줄여줘야 한다
routing table 의 크기를 줄여주는 방법은 여러가지가 있는데 그중에 대표적인 하나가 요약 이다
 
요약 

routing table 의 크기를 줄여주기 위해서
-routing table 유지를 위한 CPU 소모율이 줄어든다
-update 를 위한 대역폭 소비량이 줄어든다
=> 결론적으로 장비 소모량이 줄어든다


요약 종류

자동 요약 (classful 하게 요약) classful : subnetmask 를 무시 => default subnetmask 를 사용한다 

172.16.8.0  /24  ~  172.16.15.0  /24

172.16.0.0  /16


수동 요약 (classless 하게 요약) classless: subnetmask 를 참조 =>  CIDR


-공통된 부분까지만 고정
-공통  bit  까지만 고정


172.16.8.0  /24  ~  172.16.15.0  /24


172.16.00001  000.0
~~~~~~~~~~~~~~
172.16.00001  111.0

172.16.8.0  /21



172.16.249.0 /24 ~ 172.16.254.0 /24


172.16.11111  001.0
~~~~~~~~~~~~~~
172.16.11111  110.0


172.16.248.0  /21

172.16.11111  000.0
172.16.11111  001.0
172.16.11111  010.0
~~~~~~~~~~~~~
172.16.11111  111.0


10.10.0.0 /24 ~ 10.10.3.0 /24

10.10.000000  00.0
~~~~~~~~~~~~~
10.10.000000  11.0

10.10.0.0  /22

172.16.0.0/16 ~ 172.31.0.0 /16

172.0001  0000.0.0
~~~~~~~~~~~~~~
172.0001  1111.0.0

172.16.0.0  /12

172.0001   0000.0.0
~~~~~~~~~~~~~
172.0001   1111.0.0





172.16.8.0  /21    슈퍼넷팅
B클래스

192.16.8.0  /21    CIDR
C클래스



실습 방법

패킷 트레이서     시뮬
다이나밉스         애뮬 
GNS
장비

장비 접속 프로그램

SecureCRT , Putty , 하이퍼 터미널

원격 접속 포트

telnet (23) : 평문
ssh(22) : 암호화




다이나 밉스 실행

1.[CISCO 실습] 폴더 안에 tmp 폴더 안에 있는 내용을 삭제하고 Dynamips Server 를 실행

[참고]Dynamips Server 를 실행했을때 wpcap 이 없다라고 명시되면 www.winpcap.org 에서 4.1.3 버전을 
다운로드 받아서 실행하고 Dynamips Server를 실행한다

2.CCNA 를 실행

3.start R1 R2 R3

4.SecureCRT 로 구동

안되면 

-1,2,3 을 실행했는지 확인
-port 번호 학인 , telnet 127.0.0.1 확인

그래도 안되면 다시 다 종료했다가 다시 실행
그래도 안되면 폴더 삭제하고 알집 다시 풀어서 다시 실행



장비 구성 방법

GUI  :  경로 

CLI   : 명령어
          - 필수 설정 :  설정을 하지 않으면 통신이 안되는 설정 
          - 옵션 설정 :  설정을 하지 않아도 통신이 되는 설정  => 해주면 좋아 ~ 뭐가 좋아 ?


RAM : 설정을 하면 자동적으로 RAM 에 저장이 되고 장비는 RAM 에 있는 내용대로 동작을 한다  휘발성 메모리 : 재부팅을 하면 무조건 삭제가 된다

NVRAM : 명령어를 입력해야만 저장이 되고 명령어를 입력해야만 삭제가 된다 
           비 휘발성 메모리 : 재부팅으로 삭제가 되지 않는다  (save file 로 생각하면 된다)


NVRAM  참조 여부

config-register 값

0x2102 : NVRAM 을 로드 하는 값
0x2142 : NVRAM 을 로드 하지 않는 값


[참고] 0x 뒤에 숫자는 16진수 



Router 의 외부 구조

관리 목적

console : 관리자 포트 (rollover,rolled , 관리자,콘솔 케이블 연결)

aux : 관리자 포트 (모뎀을 이용한 원격 접속) 거의 사용되지 않고 콘솔의 백업정도로 쓰임

통신 목적

Serial  : WAN 구간 연결 , ip 주소 설정이 필요( 주로 통신 목적)

Ethernet : 주로 LAN 구간 연결 , mac 주소 통신(mac 주소가 설정이 되어 있다) ip주소 설정이 필요(주로 ARP)





CISCO IOS 기본 명령어

시스코 기준

1.시스코는 축약 단어를 지원한다. 지원할 뿐만 아니라 추천한다 즉 사용해라 

2.시스코는 기본적으로 내용을 삭제한다거나 동작을 멈추거나 아니면 동작은 반대로 할 경우에 똑같은 상황(mode , 명령어) 앞에 no 를 쓰면 된다 

3.시스코는 기본적으로 설정 순서가 상관이 없다 

4.시스코는 설정이 기본적으로 덮어씌어지지 않는다 


mode : 생김새 , 이름 , 하는 일 , 다음 모드로 넘어가는 명령어 , 명령어의 축약 단어


Router>en                                       user mode , 사용자 모드
Router#                                           privilege mode , 관리자 모드


Router#정보 확인 , 저장(copy run start) , 삭제(erase start) , 재부팅(reload) ,ping test 및 traceroute, telnet 및 ssh 접속 , clear 등등


정보 확인

show  : 정적 정보 확인
          - 그때 그당시에 그 상황에 대해서만 정보 확인이 가능 
             그래서 변화가 생기면 계속 확인을 해야 한다 

debug : 동적 정보 확인
        - 명령어에 따라 다르지만 시간 혹은 변화에 따른 정보 확인을 지속적으로 확인이  가능 
            그래서 필요하면 확인하고 필요 없으면 종료


Router>en 
Router#conf t
Router(config)#configuration global mode , 설정 모드


Router>en 
Router#conf t
Router(config)#전반적인 설정 및 상세 설정 모드로의 접근

Router>en
Router#conf t
Router(config)#line c 0
Router(config-line)#exit
Router(config)#line c 0
Router(config-line)#end  or Ctrl+z
Router#


정보 확인

sh ip route : IPv4 unicast routing table 의 정보 확인

sh ip int bri : 장비의 모든 interface 의  간략한 정보 확인


 L1                                      L2
Status                                Protocol
administratively down          down     :shutdown 상태 => no shutdown 해주면 된다

down                                  down    : L1계층 문제(cable 문제,상대방이  shutdown)

up                               down   : L2계층 문제(clock rate 문제,캡슐화 protocol 미스 매치)

up                                        up       : L2 계층까지 문제 없다


sh  run : RAM 상에 설정된 전체적인 정보 확인
sh start : NVRAM 상에 저장된 전체적인 정보 확인



sh cdp nei [detail] : 상대방 장비 정보[상세하게]를 확인 , L2 까지 up이 되어있어야 한다
sh int [s1/0]:[해당] interface 의 전체 정보 확인
sh ip int [s1/0] :ip가 동작하는 [해당]interface 의 정보 확인



IOS upgrade , backup 을 할때
-IOS 버전 정보 확인: sh ver
-Flash memory 정보  확인 : sh fla


sh clock  : 장비 시간 정보 확인
sh controllers [s1/0]: 해당 interface 에 연결된 cable 정보 확인 (cable 의 type)

sh users : 장비에 접속한 사용자 정보 확인 

sh privilege : privilege 레벨 정보 확인(범위:0~15(15만 관리자 레벨))


sh history all : 입력했던 모든 명령어 확인 



RAM 을 NVRAM 에 저장하는 명령어 : copy run start  , wr me  , wr

NVRAM 을 삭제하는  명령어 : erase start , erase nvram

재부팅 : reload












설정

설정은 필수 설정과 옵션 설정을 구분해서 외운다
          - 필수 설정 :  설정을 하지 않으면 통신이 안되는 설정 
          - 옵션 설정 :  설정을 하지 않아도 통신이 되는 설정  => 해주면 좋아 ~ 뭐가 좋아 ?
+mode 까지 외워야 한다




password 설정 (옵션 설정 : 장비 접속에 대한 보안이 좋아진다)

1>enable (주의점:password 의 대소문자 구분되고 스페이스 바도 입력이 된다)

- secret : 암호화 , 우선 순위가 높다    설정  : enable secret cisco
- 일반   :  평문 , 동일하면 안된다        설정 :  enable pass soldesk

2>line

login 유무에 따라서 password 입력 유무가 정해짐 


line c 0
pass cisco
login

Router con0 is now available

Press RETURN to get started.

User Access Verification

Password:cisco 
Router>


==========================================================

login 유무에 따라서 password 입력 유무가 정해짐 


line a 0
pass cisco
login

==========================================================

login 유무에 따라서 password 입력 유무가 정해짐 
password 입력 유무에 따라서 접속 유무가 정해짐 


line v 0 4
pass cisco
login



R1#telnet 13.13.12.2
Trying 13.13.12.2 ... Open

User Access Verification

Password: cisco
R2>


[참고]

loopback interface : 가상 interface로 실제 DATA를 송수신 불가능 하다

-관리 목적: ping test , telnet or SSH 같은 원격 접속 가능 ,  IOS upgrade or IOS backup 등을 할때
ip 가 필요하다 물리적인 interface 는 변경이나 피해를 볼수 있지만 loopback interface 는 물리적으로 
피해를 볼일이 없다 그래서 관리 목적으로  loopback interface 를 사용하자



interface 설정 (필수 설정: CCNA의 기본 설정)

R1

ho R1

int lo 172
ip add 172.16.1.1 255.255.255.0

int f 0/0
ip add 13.13.10.1 255.255.255.0
no shut

int s 1/0
ip add 13.13.12.1 255.255.255.0
no shut

R2

ho R2

int f 0/0
ip add 13.13.20.1 255.255.255.0
no shut

int s 1/0
ip add 13.13.23.2 255.255.255.0
no shut

int s 1/1
ip add 13.13.12.2 255.255.255.0
no shut


R3

ho R3

int lo 172
ip add 172.16.3.1 255.255.255.0

int f 0/0
ip add 13.13.30.1 255.255.255.0
no shut

int s 1/1
ip add 13.13.23.3 255.255.255.0
no shut


[참고]
loopback interface 는 삭제할때 no int lo 172

물리적인 interface 삭제는 불가능하고 설정된 내용 삭제는  default int f 0/0   + shutdown


[참고]

int s 1/0
no shut                                           L1 설정 
clock rate 64000                               L2 설정 
encapsulation hdlc                           L2  설정(cisco 는 기본 HDLC)
ip add 192.168.1.1 255.255.255.0       L3 설정

[참고]

interface 설정이 끝나고 난후

1>sh ip route 확인 , 문제가 없으면 2>을 실행 , 문제가 있으면 4>을 실행

2>구간 마다 ping test , 문제가 있으면 4>을 실행

3>문제가 없으면 끝

4>sh ip int bri , sh run 으로 T/S 실행



기타 옵션 설정

no ip domain-lookup   불필요한 DNS 요청 방지

line c 0
logging synchronous    줄정리
exec-t 0 0                    콘솔 종료 X

en
conf t
no ip domain-lo
line c 0
logging sy
exec-t 0 0
exit


Router 는 Routing

Routing

Router 가 IP 헤더안에 있는 목적지 ip 를 보고 routing table 을 참조해서 목적지 방향쪽 interface 로 packet 을 전송

+목적지까지 책임을 지는 것이 아니라 다음 router 까지만 책임을 진다

routing table 을 참조

1> routing table 에 정보가 있으면 전송이 가능 
     routing  table 에 정보가 없으면 전송이 불가능 

=> routing table 을 완성 

목적지까지 책임을 지는 것이 아니라 다음 router 까지만 책임을 진다

=> 모든 router 가 모든 network 정보를 가지고 있어야 한다

[routing table 을 완성]

1.interface 설정을 한다

=> routing table 에 등록 : 1>ip 대역대가 있어야 한다 2> L2 까지 up이 되어야 한다

interface 설정을 해서 routing table 에 등록이 되면 routing table 에는 물리적이든 논리적이든 직접 연결된 network 즉 directly connected 만 routing table 에 등록이 된다

즉 routing table 이 전체적으로 완성이 되질 않았다
routing table 을 완성 시켜주기 위해서 routing protocol 을 구동 시켜 준다

Routing protocol 의 종류

-Static : 남의 이름 물어보기 

-Dynamic
 -IGP  : 자기 소개하기 
 -EGP : 우리반 소개하기 



Static 

내가 모르는 네트워크를 관리자가 일일이 설정 (남의 이름 물어보기)

장점
-보안성,신뢰성,예측 가능성이 좋다
-경로 계산을 위한 CPU 소모율이  없다 
-update 를 위한 대역폭 소비량이 없다 

단점

-확장성이 떨어진다
-변화에 적응이 느리다
-설정 유지가 어렵다

 
소규모 네트워크 ,유동적이지 않은 네트워크,보안을 생각하는 네트워크,관리자가 마음대로 하고 싶은 네트워크,장비 사양이 떨어지는 경우
(백업용)



### 설정 

ip route [내가 모르는 네트워크'네임][netmask][next hop'ip]

or

ip route [내가 모르는 네트워크 ' 네임][netmask][발신 interface 의 이름]




R1

ip route 13.13.20.0 255.255.255.0 13.13.12.2
ip route 13.13.23.0 255.255.255.0 13.13.12.2
ip route 13.13.30.0 255.255.255.0 13.13.12.2
ip route 172.16.3.0 255.255.255.0 13.13.12.2

R2

ip route 172.16.1.0 255.255.255.0 13.13.12.1
ip route 13.13.10.0 255.255.255.0 13.13.12.1
ip route 172.16.3.0 255.255.255.0 13.13.23.3
ip route 13.13.30.0 255.255.255.0 13.13.23.3


R3


ip route 172.16.1.0 255.255.255.0 13.13.23.2
ip route 13.13.10.0 255.255.255.0 13.13.23.2
ip route 13.13.12.0 255.255.255.0 13.13.23.2
ip route 13.13.20.0 255.255.255.0 13.13.23.2



-default  static 

설정

ip route 0.0.0.0 0.0.0.0 [next hop'ip]

or

ip route 0.0.0.0 0.0.0.0 [발신 interface 의 이름]



Routing


Router 가 IP 헤더안에 있는 목적지 ip 를 보고 routing table 을 참조해서 목적지 방향쪽 interface 로 packet 을 전송

+목적지까지 책임을 지는 것이 아니라 다음 router 까지만 책임을 진다


routing table 을 참조

1> routing table 에 정보가 있으면 전송이 가능 
     routing  table 에 정보가 없으면 전송이 불가능 

### 경로검색
2> 경로 검색 => 경로 선출 => 경로 유지

경로 검색, 경로 선출, 경로 유지를 관리자가 일일이 지정하는 것은 static routing protocol
경로 검색, 경로 선출, 경로 유지를 router 안에서 routing protocol 이 알아서 하는 것은 dynamic routing protocol 이다



경로 선출

###
1.롱기스트 매치룰 : 목적지 ip 에 가장 길게 일치하는 경로가 선출

목적지 ip : 172.16.1.1

172.16.1.0 /24  경로 선출
172.16.0.0 /16

###
2.상황에 따라서 

-다수의 routing protocol 이 있는 경우 AD(신뢰도)값이 가장 작은 경로가 선출

목적지 ip : 172.16.1.1

172.16.1.0 /24   AD  110    경로 선출
172.16.1.0 /24   AD  120


[참고]
routing protocol 의 AD 값은 변경할수 있다 


-하나의(동일한) routing protocol 이 있는 경우 metric(경로값)값이 가장 작은 경로가 선출

목적지 ip : 172.16.1.1

172.16.1.0 /24   AD  110   M = 64     경로 선출
172.16.1.0 /24   AD  110   M =  128

[참고]
dynamic routing protcol 의 metric 은 변경할수 있다 


[추가]

next hop 이 보장이 되지 않으면 network 정보를 routing table 에 등록할수가 없다
=> IGP 에서는 conneted 로 기본 보장이 된다

## 5부 라우터 개념

Router 가 사용하는 스위칭 방식
=> routing table 참조 여부

-Process switching : DATA 를 전송할때마다 매번 routing table 을 참조하는 방식 

-Fast switching :처음에만 routing table 을 참조하면서 자신의 캐시table 에 복제하고 이후에는 캐시 table 을 참조해서 DATA  전송

-CEF : routing table 이 완성이 될때 자신의 CEF table 에 복제를 하고 CEF table 을 참조해서 DATA 를 전송 
         즉 rouing table 을 한번도 참조하지 않는다

routing table 을 매번 참조하든 아니든 routing table 에 있어야만 복제를 할수가 있다 
즉 routing table 에 정보가 있어야 통신이 가능하다 없으면 통신이 불가능


[참고]
로드 분산을 하는 경우의 차이

-Process switching : 매번 차례대로 진행을한다
-Fast switching :목적지 ip 주소에 따라서 경로가 달라진다
-CEF : 출발지 ip , 목적지 ip 주소에 따라서 경로가 달라진다 

+ CEF : ip load-sharing per-packet 을 로드 분산할 interface 설정을 하면 패킷별로 로드 분산이 된다  


AS (Autonomous  System)

동일한 혹은 하나의 정책이 동작하는 네트워크(동일한 관리자에 의해서 관리가 되는 router 의 집단,모임)
=> 지역 단위

IGP  : AS 안에서 빨리 빨리가 목적
EGP : AS 와 AS 사이에서 많이 많이가 목적



Routing


Router 가 IP 헤더안에 있는 목적지 ip 를 보고 routing table 을 참조해서 목적지 방향쪽 interface 로 packet 을 전송

+목적지까지 책임을 지는 것이 아니라 다음 router 까지만 책임을 진다


routing table 을 참조

1> routing table 에 정보가 있으면 전송이 가능 
     routing  table 에 정보가 없으면 전송이 불가능 

2> 경로 검색 => 경로 선출 => 경로 유지

경로 검색, 경로 선출, 경로 유지를 관리자가 일일이 지정하는 것은 static routing protocol
경로 검색, 경로 선출, 경로 유지를 router 안에서 routing protocol 이 알아서 하는 것은 dynamic routing protocol 이다

routing table 을 완성

interface  설정
=>interface 설정이 routing table 에 등록이 되려면 
1>ip 대역대가 있어야 한다
2>L2 까지 up 이 되어있어야 한다

interface 설정

HDLC  기반

int s 1/0
ip add 192.168.1.1 255.255.255.0
no shut

+ DCE 가 연결된 serial interface 에는 clock rate 값을 설정해줘야 한다

[참고]  계층순서대로 설정

int s 1/0
no shut                                                 L1 설정
clock rate 64000                                     L2 설정
encapsulation hdlc                                  L2 설정
ip add 192.168.1.1 255.255.255.0              L3 설정

interface 가 routing table 에 등록이 되면 routing table 에는 직접 연결된 network 정보만 등록

즉 routing table 이 전체적으로 완성이 되질 않는다
그래서  routing table 을 완성 시키려면 routing protocol 을 구동 시켜준다

routing protocol 종류

-Static : 내가 모르는 네트워크를 관리자가 일일이 설정 (남의 이름 물어보기)

설정


ip route [내가 모르는 네트워크 ' 네임][netmask][next hop 'ip]

or

ip route [내가 모르는 네트워크 ' 네임][netmask][발신 interface 의 이름]


###
-Dynamic 

  IGP : 내 네트워크를 관리자가 설정해주면 알아서 동적으로 전파 (자기 소개하기)
  -distance vector : Ripv1,Ripv2
  -link - state : OSPF , IS-IS
  -advance distance vector : EIGRP


  EGP : 본인의 routing table 에 있는 정보를 관리자가 설정하면 알아서 동적으로 전파 (우리반 소개하기)
  -path vector : BGPv4 

 

[참고]
routing protocol 의 T/S 기본 방법

전체 네트워크가 7개면  routing table 이 기본 7개가 나와야 한다 
근데 7개가 나오지 않으면 문제가 있다라고 인식한다 그리고
routing table 에 없는 네트워크 정보를 찾는다

-static 일 경우
 그 라우터에서 제대로 그 네트워크를 설정해줬는지  sh run 으로 확인

-dynamic 일 경우
 routing table 에 없는 네트워크를 가진 router 를 찾은 후에 그 router 에서 제대로 설정 해줬는지 sh run 으로 확인



    distance vector

주기적으로 인접한 router 에게만 routing table 전체를  update 한다

update 를 위한 대역폭 소비량이 많다
update 를 위한 CPU 소모율이 많다 
=> 장비 소모량이 많다

구조가 간단하다
확장성이 떨어진다
변화에 적응이 느리다
알고리즘상 루프가 발생을 한다
(루프 방지법:Split-Horizon : 수신한 정보를 수신한 interface 로 다시 전송하지 않는다)


## 6부

Ripv1

1.개방형 
2.AD  120
3.UDP = 520
4.classful routing protocol
5.VLSM,CIDR 지원 X
6.자동 요약만 지원 
7.broadcast update (255.255.255.255)

8.update 주기 시간                      : 30 초
   invaild time(수신 대기 시간)       : 180초 
   holddown time(삭제 대기 시간)  : 180초
   flushed time (총 삭제 시간)        : 240초

9.균등 로드 분산만 지원 (기본 4개 ~ 최대 16개) 범위 : 1 ~ 16 까지 조절이 가능 

10.metric = hop  count = Router 경유 수(범위:1 ~ 15) 16이면 limit 라고 해서 장애 발생으로 인식



11.설정

ripv1 은  classful 로 동작 , 설정은 classful 하게 설정

[주의]동작과 설정은 별개

172.16.1.0 /24
13.13.10.0 /24
13.13.12.0 /24

router rip 
v 1
net 172.16.0.0
net 13.0.0.0



Ripv1                                                                      Ripv2 

classful  routing protocol                                           classless routing protocol
VLSM,CIDR 지원 X                                                     VLSM,CIDR 지원 O
자동 요약만 지원                                                       자동,수동 요약 둘다 지원 ,기본은 자동 => 끄자
broadcast update (255.255.255.255)                            multicast  update (224.0.0.9)

옵션                                                                        옵션 

triggered  update 지원 X                                       triggered  update 지원 O (WAN 구간 P2P 구간만 지원)
해시함수를 이용한 MD5 인증 기능 X                          해시함수를 이용한 MD5 인증 기능 O


인증이 제대로 될경우는 DATA 를 수신
인증이 제대로 안되었을 경우는 DATA 를 폐기




Ripv2 필수 설정

동작은 classless , 설정은 classful 하게 설정

172.16.1.0 /24
13.13.10.0 /24
13.13.12.0 /24

router rip
v 2
net 172.16.0.0
net 13.0.0.0
no au



Ripv2  옵션 설정

1> triggered  update 설정 (WAN 구간 P2P 구간만 지원)


triggered  update 를 할 구간에 연결된 모든 interface 에서 설정

R1
int s 1/0
ip rip triggered

R2
int s 1/1
ip rip tr

triggered  update 를 설정을 하면 주기적인 update 를 하지 않는다
변화가 생겼을때만 update 를 해준다



2>해시함수를 이용한 MD5 인증 설정


1.인증할 구간에 연결된 모든 router 에서 key chain 을 설정한다

key chain AAA                서로 달라도 상관이 없다
key 13                            서로 동일해야 한다  
key-string cisco               서로 동일해야 한다

2.인증할 구간에 연결된 모든 interface 에서 key-chain 을 적용한다

R1
int s 1/0
ip rip authentication key-chain AAA
ip rip authentication mode md5

R2
int s 1/1
ip rip au k AAA
ip rip au m m




3>수동 요약 설정

요약 설정이 필요한 이유 : routing table 의 크기를 줄여주기 위해서
=> update 를 위한 CPU 소모율 줄어들고 , update 를 위한 대역폭이 줄어든다
=> 장비 소모량이 줄어든다

요약이 되면 NULL 경로가 필요한다 즉 NULL 경로가 생성이 되어야 한다
기본적으로 자동 생성이 되는데 RIPV2 는 자동 생성이 되지 않는다 => 수동 생성을 해야 한다

NULL 경로가 생성되어야 하는 이유는 루프를 방지 

Ripv2 는 수동 생성

ip route [요약 내용][netmask] null 0


요약 설정

요약을 넘겨줄 interface 에 설정


int s 1/0
ip summary-address rip [요약내용] [netmask]



ex>

168.16.8.0 /24 ~ 168.16.15.0 /24


공통 bit 까지만 고정

168.16.00001  000.0
~~~~~~~~~~~~~~
168.16.00001  111.0

168.16.8.0 /21 = 255.255.248.0

R1
int s 1/0
ip summary-address rip 168.16.8.0 255.255.248.0


clear ip route *  : Routing table 재시작 , 정리 
             
=> ripv1 or ripv2 에서 빨리 진행이 안되면 해준다


[전체 옵션]

passive-interface : 불필요한 update traffic 의 낭비를 막기 위해서 사용

동작

passive-interface로  지정된 interface 로는 update 를 안함 , 단 수신은 한다


설정

router mode 에서 설정

-router)#passive-interface lo 172
-router)#passive-interface f 0/0

or

-router)#passive-interface default
-router)#no passive-interface s1/0


[정리] 

split-horizon : 수신한 정보를 수신한 interface 로 다시 전송하지 않는다

ripv1
=>classful 로 동작(subnetmask 를 무시)= > 사용 X
설정: classful 하게 설정

router rip
v 1
net 172.16.0.0
net 13.0.0.0

ripv2
=>classless (subnetmask 를 인정)
설정 : classful 하게 설정

router rip
v 2
net 172.16.0.0
net 13.0.0.0
no au  =>(자동,수동 둘다 지원,기본은 자동 => 끄자)

[참고]
설정과 동작은 별개


Ripv2 옵션

triggered update (변화가 있을때 update해주는 방식)

설정은 triggered update 할 구간에 연결된 interface 에서 설정

R1
int s 1/0
ip rip tr

R2
int s 1/1
ip rip tr


MD5 인증 설정
(인증:무결성을 보장 => 문제가 있으면 폐기)

요약 설정
요약 설정을 하면 null 이 생성되어야 한다
기본적으로 자동 생성이 된다
Ripv 2 는 자동 생성이 되지 않는다 => 수동적으로 생성(설정)해야한다

null 이 생성되어야 하는 이유 : 기본적으로 루프 방지




EIGRP

    Link  -  state 

1.Link 변화시 인접성을 맺은 모든 router 에게 변화된 내용만 update 를 한다

-update 를 위한 대역폭 소비량이 적다
-update 를 위한 CPU 소모율이 적다
-구조가 복잡 (인접성)
-확장성이 좋다
-변화에 적응이 빠르다

2.classless routing protocol 
-VLSM,CIDR 지원

3. multicast  update 

OSPF  :  224.0.0.5 ~ 6



[참고]

OSPF    224.0.0.5 ~ 6
Ripv2    224.0.0.9
EIGRP   224.0.0.10


## EIGRP
EIGRP

1.cisco  전용 (2013 년 이후에는 RFC 등록)
2.classless routing protocol
3.VLSM,CIDR 지원 된다
4.자동,  수동 요약 둘다 지원, 기본은 자동(classful 의 문제점 발생) => 끄자
5.multicast  update  :  224.0.0.10
6.AD : 5(summary)  90(internal)   170(external)

7.균등,비균등 로드 분산 둘다 지원
(기본은 균등 로드 부산만 지원 , 비균등 로드 분산을 하려면 variance 값을 조절해줘야 한다 ,기본값 1이고 범위는 1 ~ 128 )


[참고] 12:50 PM
비균등 로드 분산을 하려면 2가지의 조건이 만족 되어야 한다

1>variance 값을 이용해서 최적 경로의 metric 보다 비균등 로드 분산 하려는 경로의 metric 을 작게 만들어 준다

2>최적 경로의 FD 보다 작은 AD 값을 가지고 있어야 한다(후속 경로)



8.metric 

-K metric : K-value , K상수

  K1=1  , K2=0 , K3=1 , K4=0 , K5=0 

-Vector metric

 bandwidth  : 대역폭
 delay         : 지연
 Reliability   : 신뢰성 
 Load          : 과부하
 MTU          : 전송 최대 크기 유닛


(K1 x Bandwidth) + [(K2 x Bandwidth) / (256 - Load)] + (K3 x Delay)


Bandwidth , Delay

10^7/bw * 256 + Delay/10 * 256 = 32bit

 BW  : 최소 BW
delay : 합



9.인접성

Hello : 인접성을 맺고 유지(인접성의 조건:K-value , AS -number,인증) 
           유지 시간이 3배 (hold : hello 수신 대기 시간)

Update : 정보를 update 할때 

Query : 네트워크에 장애가 생겼을 경우 정보를 요청 
+update 를 준 router에게만 Query 를 요청 

Reply : Query 에 대한 응답

Ack : 수신 확인 , 승인


인접성이 해지 되는 경우

1.hold 시간 안에 hello 를 수신하지 못하는 경우는 인접성을 해지 한다

2.update , Query ,Reply 는 ack 를 수신해야 한다
   수신하지 못하면 16번을 재전송을 하고 그래도 수신하지 못하면 인접성을 해지 한다

3,Query 를 보내면 reply 를 수신해야 한다
   수신하지 못하면 SIA(Stuck In Active) 로 3분이 지나면 인접성이 해지가 된다


10. 3개의 table 

Neighbor  table  : 네이버에 관한 정보(인접성을 맺은 router 의 정보)   :  sh  ip eigrp nei

Topology  table : 네이버에게 받은 정보 (인접성을 맺은 router 를 통해서 들어오는 network 정보)  : sh ip eigrp to

Routing table  : 최적 경로가 등록된 table  : sh ip route



FD = Metric :출발지 router 부터 목적지 router 까지의 경로값 

AD = Source Metric :출발지 router랑 인접성을 맺은router부터 목적지router까지의 경로값


S(최적 경로) 와 FS (후속 경로) 선출 기준

1.FD 값이 가장 작은 경로가 S(최적 경로) 가 된다

2.FS (후속 경로)는 S(최적 경로) 의 FD 값보다 작은 AD 값을 가진 경로


11.Network type
                            Hello          Hold 
                      
point-to-point           5              15 
broadcast                  5              15
nonbroadcast           60            180


###
12.설정

classful 하게 설정

172.16.1.0 /24
13.13.10.0 /24
13.13.12.0 /24

router eigrp 100
net 172.16.0.0
net 13.0.0.0
no au


classless 하게 설정

172.16.1.0 /24
13.13.10.0 /24
13.13.12.0 /24

router eigrp 100
net 172.16.1.0 0.0.0.255
net 13.13.10.0 0.0.0.255
net 13.13.12.0 0.0.0.255
no au

[설정과 동작은 별개]



Wildcard Mask (EIGRP , OSPF , ACL)
=> 설정을 최소화 



Wildcard Mask  와 Subnetmask 의 공통점

=> ip 를 규정해준다

Wildcard Mask  와 Subnetmask 의 차이점 


1.표기법의 차이


S      1       0

W     0       1

255.255.255.0 => 11111111.11111111.11111111.00000000
                          00000000.00000000.00000000.11111111  => 0.0.0.255

255.255.255.255
255.255.255.0
    0.    0.   0.255


ex> /30 => 255.255.255.252 => 0.0.0.3


2.bit 의 불연속 가능 유무

S    불가능 

W    가능


Wildcard Mask 를 구하는 방법
=>  공통된 부분(공통bit) 는 0 으로 고정
      공통된 부분(공통bit)가 아니면 1로 안고정




192.168.0.0 /24 ~ 192.168.255.0 /24 에서 각각의 네트워크 ip 중에서 사용할수 있는 첫번째 ip만 지정하여라

192.168.0.1  255.255.255.255
192.168.1.1  255.255.255.255
192.168.2.1  255.255.255.255
~~~~~~~~~~~~~~~~~~~~~
192.168.255.1 255.255.255.255

192.168.0.1  0.0.255.0 


192.168.1.0  /24 의 ip 중에서 홀수만 지정

192.168.1.1  255.255.255.255
192.168.1.3  255.255.255.255
192.168.1.5  255.255.255.255
~~~~~~~~~~~~~~~~~~~~~~
192.168.1.255  255.255.255.255

192.168.1.00000001
192.168.1.00000011
192.168.1.00000101
~~~~~~~~~~~~~~
192.168.1.11111111

192.168.1.1  0.0.0.254    => 홀수만 지정


192.168.1.00000000
192.168.1.00000010
192.168.1.00000100
~~~~~~~~~~~~~~
192.168.1.11111110

192.168.1.0  0.0.0.254  => 짝수만 지정



192.168.1.129  /24 ~ 192.168.1.131  /24 

192.168.1.10000001
192.168.1.10000010
192.168.1.10000011

192.168.1.128  0.0.0.3

192.168.1.129  /24 , 192.168.1.131  /24


192.168.1.100000 0 1
192.168.1.100000 1 1

192.168.1.129  0.0.0.2

[주의]
단 ACL 에서만 bit 의 불연속이 가능하다 eigrp 와 ospf 는 불가능하다




EIGRP 필수 설정


classful 하게 설정  => 불필요한 정보도 업데이트가 될수 있다(보안적으로 좋지않다)

172.16.1.0 /24
13.13.10.0 /24
13.13.12.0 /24

router eigrp 100
net 172.16.0.0
net 13.0.0.0
no au

classless 하게 설정

172.16.1.0 /24
13.13.10.0 /24
13.13.12.0 /24

router eigrp 100
net 172.16.1.0 0.0.0.255
net 13.13.10.0 0.0.0.255
net 13.13.12.0 0.0.0.255
no au



EIGRP 옵션 설정

해시함수를 이용한 MD5 인증 설정


1.인증할 구간에 연결된 모든 router 에서 key chain 을 설정한다

key chain AAA                서로 달라도 상관이 없다
key 13                            서로 동일해야 한다  
key-string cisco               서로 동일해야 한다

2.인증할 구간에 연결된 모든 interface 에서 key-chain 을 적용한다

R1
int s 1/0
ip authentication key-chain eigrp 100 AAA
ip authentication mode eigrp 100 md5

R2
int s 1/1
ip authe k e 100 AAA
ip authe m e 100 m


수동 요약 설정

요약 설정이 필요한 이유 : routing table 의 크기를 줄여주기 위해서
=> update 를 위한 CPU 소모율 줄어들고 , update 를 위한 대역폭이 줄어든다
=> 장비 소모량이 줄어든다

요약이 되면 NULL 경로가 필요한다 즉 NULL 경로가 생성이 되어야 한다
기본적으로 자동 생성이 되는데 RIPV2 는 자동 생성이 되지 않는다 => 수동 생성을 해야 한다

NULL 경로가 생성되어야 하는 이유는 루프를 방지 

요약 설정

요약을 넘겨줄 interface 에 설정


int s 1/0
ip summary-address eigrp 100 [요약내용] [netmask]



ex>

168.16.8.0 /24 ~ 168.16.15.0 /24


공통 bit 까지만 고정

168.16.00001  000.0
~~~~~~~~~~~~~~
168.16.00001  111.0

168.16.8.0 /21 = 255.255.248.0

R1
int s 1/0
ip summary-address eigrp 100 168.16.8.0 255.255.248.0


[참고]

neighbor table 은 네이버에 관한 정보(즉 인접성을 맺은 Router 의 정보)
네이버에게 받은 정보(인접성을 맺은 router 에게 받은 network 정보)는 Topology table 에 등록을 하고 Dual 알고리즘을 통해서 최적 경로를 선출하고 선출된 경로를 Routing table 에 등록하고 Router 는 Routing table 을 참조해서 통신을 한다


Router - id (EIGRP , OSPF , BGPv4)

Router 를 구분하는 식별자 (IPv4 주소 형식으로만 진행*IPv6 에서도 동일하다)

Router - id 선출 기준

1.설정

router eigrp 100
eigrp router-id 1.1.1.1

2.loopback interface 의 ip 중에서 숫자가 가장 큰 ip 가 router-id 로 선출

3.물리적인 interface 의 ip 중에서 숫자가 가장 큰 ip 가 router-id 로 선출




OSPF (Open Shortest Path First)

Link - State 에 속해있는 SPF 알고리즘을 사용하는 대표적인 개방형 Routing Protocol 이다



    Link  - State


1.Link 변화시 인접성을 맺은 모든 router 에게 변화된 내용만 update 를 한다


[참고]
1> triggered update (변화가 생기면 정보를 최대한 빨리 update 한다)
2> 네트워크 정보의 출처까지 포함해서 update 한다
 =>즉 각각의 Router 에서 전체적인network 를  판단할수가 있다( database table 에 있다)

-update 를 위한 CPU 소모율이 적다
-update 를 위한  대역폭 소비량이 적다

=> 변화가 많으면 오히려 장비 소모량이 많아진다
     (해결 방안 : 하나의 AS 안에 여러 area 로 구분을 하는 2계층 구조를 가진다)


-구조가 복잡 (인접성)

  =>인접성을 맺어야만 정보를 update 한다
      즉 인접성을 맺지 않으면 정보가 교환되지 않는다 
      그래서 인접성을 맺는 것들은  제일 먼저 인접성을 맺었는지 확인


-확장성이 좋다
-변화에 적응이 빠르다

[참고]

distance vector  : slow
link - state : fast
eigrp : very fast


2.classless routing protocol

-VLSM,CIDR 지원 된다  => 수동요약만 지원한다 

3.multicast update


OSPF     224.0.0.5~6 

[참고]

OSPF     224.0.0.5~6 
Ripv2     224.0.0.9
EIGRP    224.0.0.10


OSPF (Open Shortest Path First)

Link - State 에 속해있는 SPF 알고리즘을 사용하는 대표적인 개방형 Routing Protocol 이다

1.AD 110
2.Version  2   참고 : IPv6 OSPF (Version 3)
3.개방형 
4.classless routing protocol
5.VLAM,CIDR 지원 O
6.수동 요약만 지원 (no au 하면 안됨)
7.multicast update 224.0.0.5~6 (Hello : 224.0.0.5)

[참고]
수동적으로 neighbor 이라는 명령어로 인접성을 맺게 되면 unicast 로  update 가 된다

8.균등 로드 분산만 지원 (기본 4개 ~ 최대 16개) 범위 : 1 ~ 16  ( sh ip protocol )


9.metric = COST = 10^8/BW  =  100M/BW
[참고]
10^7 = 10M , 10^8 = 100M , 10^9 = 1000M

   10M  = 10^8/10^7 = 100M/10M   = 10
  100M  = 10^8/10^8 = 100M/100M   = 1   경로 선출

  100M  = 10^8/10^8 = 100M/100M    = 1
 1000M  = 10^8/10^9 = 100M/1000M   = 1   불필요한 균등 로드 분산 


불필요한 균등 로드 분산을 해결하려면 

auto-cost reference-bandwidth 명령어를 사용

router ospf 1
auto-cost reference-bandwidth  1000

설정을 하면 100M/BW 를 1000M/BW 로 변경

  100M  = 10^9/10^8 = 1000M/100M    = 10
 1000M  = 10^9/10^9 = 1000M/1000M   =  1    경로 선출


10. 2계층 구조 
(계층적 구조 : 하나의 AS 안에 여러 area  로  구분)

- area 0 은 backbone area 이고 서로 다른 area 가 통신 하려면 area 0 을 통해서 통신할수 있다 즉 일반 area 들은 area 0 에 연결이 되어있어야 한다

=>물리적으로 연결이 되어있지 않으면 Virtual-link 설정을 해줘야 한다
   (방향쪽 ABR 과 물리적으로 연결되어있지 않은 area 의 경계 Router 에서 설정)

- area 의 범위 : 0 ~ 4294967295
- area 안에 Router 는 최대 40 에서 50대 정도 권장
- area 0 과 일반 area 사이에 있는 Router 는  ABR ( Area Border Router )
- ABR 은 물리적으로 2개의  area 만 포함하기를 권장


11.인접성

Hello   : 인접성을 맺고 유지(인접성의 조건) 유지시간 4배차이 
DBD    : 전체적인 정보를 교환 
LSR     : 새로운 정보를  요청
LSU     : LSR 에 대한 응답
LSA     : 승인

Hello 

Router-id  : Router 구분하는 식별자 
=> 서로  동일하면 인접성을  맺을수 없다

DR,BDR  주소 
Priority (우선 순위값) = 기본값 1 (범위 : 0 ~ 255)
[주의점] Priority값이 0이면 절대로 DR ,BDR 되지 않는다
subnetmask
neighbor's list

area-id (area 번호) => 서로 동일해야 한다
authentication password(인증 암호) => 서로 동일해야 한다
-무인증(0) 평문 인증(1) MD5인증(2)
Hello,Dead(Hello 수신대기 시간) interval(주기)4배차이 => 서로 동일 해야 한다
stub area flag : stub 으로 지정된 area 안에 있는 모든 router 는 stub 이라고 설정 
=> 서로 동일해야 한다

MTU : 전송 최대 크기 유닛 => 서로 동일해야 한다



Router - id (EIGRP , OSPF , BGPv4)

Router 를 구분하는 식별자 (IPv4 주소 형식으로만 진행*IPv6 에서도 동일하다)

Router - id 선출 기준

1.설정

router ospf 1
router-id 1.1.1.1

2.loopback interface 의 ip 중에서 숫자가 가장 큰 ip 가 router-id 로 선출

3.물리적인 interface 의 ip 중에서 숫자가 가장 큰 ip 가 router-id 로 선출

+ 인접성을 맺으면 더 좋은 조건의 내용이 와도 변경되지 않는다
   단 재인접성을  (reload  or clear ip ospf process ) 맺으면 선출 기준에 따라서 다시 선출이 된다


DR,BDR 의 선출 기준

1.Priority = 1 ( 0~255 ) 0 이면 절대로 DR,BDR 되지 않는다
=>Priority 값이 가장 큰 Router 가 DR 이 되고 그 다음이 BDR 이 되고 나머지는 DRother 가 된다

2.Router-id 
=>Router-id  값이 가장 큰 Router 가 DR 이 되고 그 다음이 BDR 이 되고 나머지는 DRother 가 된다

+ 선출이 된 이후에는 더 좋은 조건의 내용이 와도 변경되지 않는다
   단 재인접성을  (reload  or clear ip ospf process ) 맺으면 선출 기준에 따라서 다시 선출이 된다


12.3개의 table 


Neighbor  table  : 네이버에 관한 정보(인접성을 맺은 router 의 정보)   :  sh  ip ospf nei

Database  table : 네이버에게 받은 정보 (인접성을 맺은 router 를 통해서 들어오는 network 정보)  : sh ip ospf data

Routing table  : 최적 경로가 등록된 table  : sh ip route



13.Network Type --외울것

                                Hello        Dead      DR,BDR 선출 유무     네이버(인접성)
point-to-point                 10           40                 X                     자동
broadcast                       10           40                  O                     자동
point-to-multipoint           30          120                X                    자동   
nonbroadcast                   30          120                O                     수동



14.LSA 광고 타입  -->외울것

          구분      영어 구분      정보                    출처       routing table   database  table 

1     같은 area    intra area    Router-id            Router             O               Router    
2     같은 area    intra area    DR 정보                 DR                                 Net

3     다른 area    inter area    Network정보           ABR             OIA         Summary Net
4     다른 area    inter area    ASBR 정보              ABR                            Summary Asb

5     다른 AS    AS-external   외부네트워크 정보   ASBR             OE1 : metric 증가
                                                                                          OE2 : mteric 고정 (기본)


[광고 타입 우선 순위]

1>intra
2>inter
3>E1
4>E2

 E2

 
[참고]

ABR : Area Border Router : Area 0(backbone area) 과 일반 area 사이에 있는 중계  Router

ASBR : Autonomous System Boundary Router(재분배 해준 router):OSPF 와 다른 AS 사이에 있는 중계 Router

요약은 ABR 과 ASBR 에서 할수 있다


15.설정

 OSPF 필수 설정

172.16.1.0  /24
13.13.10.0  /24
13.13.12.0  /24


router ospf 1
net 172.16.1.0 0.0.0.255 area 0
net 13.13.10.1 0.0.0.0 a 0
net 13.13.12.1 0.0.0.255 a 0


OSPF 에서 일반 area는 area 0 즉 backbone area 에 연결이 되어 있어야 한다 근데 연결이 되어 있지 않으면 물리적으로 연결되어 있지 않은 방향쪽 ABR 과 물리적을 연결이 되어 있지 않은 AREA 의 경계 Router 에서Virtual-Link 를 설정 해줘야 한다


router ospf 1
area X virtual-link [상대방 router-id]

R2

router ospf 1
area 13 virtual-link 3.3.3.3

R3

router ospf 1
area 13 v 2.2.2.2



 OSPF 옵션 설정

MD5 인증 설정

-interface 인증 설정 : 설정한 구간에서만 인증이 진행된다 
 인증할 구간에 연결된 모든 interface 에서 설정

R1
int s 1/0
ip ospf authentication message-digest
ip ospf message-digest-key 13 md5 cisco

R2
int s 1/1
ip ospf au m
ip ospf me 13 m cisco


-area 인증 설정
 인증 설정을 한 area 전체가 인증
 인증할 area안에 속해있는 모든 router 에서 설정하고 인접성을 맺은 모든 interface 에 적용


R1
router ospf 1
area 0 authentication message-digest

int s 1/0
ip ospf message-digest-key 13 md5 cisco

R2
router ospf 1
area 0 au m


int s 1/1
ip ospf me 13 m cisco

R3
router ospf 1
area 0 au m



정보 확인

interface 설정

sh ip route
sh ip int bri
sh run

sh cdp nei  det
sh int s 1/0
sh ip int s 1/0


dynamic 

sh ip protocol  


eigrp 

sh ip eigrp to
sh ip eigrp nei
sh ip eigrp traffic

ospf

sh ip ospf nei    : 네이버 관한 정보
sh ip ospf data  : 네이버에게 받은 정보
sh ip ospf int s 1/0 : OSPF가 동작하는  interface 의 정보
sh ip ospf vir  : virtual-link 의 동작 정보 

virtual-link 설정을 하기 전에 sh ip protocol,sh ip ospf nei,sh ip ospf data,sh ip route 정보를  메모장에 복사해놓고 virtual-link 설정을 다 한후에 
sh ip protocol,sh ip ospf nei,sh ip ospf data,sh ip route 정보를 확인해서 비교해라

외부 정보를 재분배하고 sh ip ospf data , sh ip pro , sh ip route 확인 




Router 는 Routing

Routing 

Router 가 IP헤더안에 있는 목적지 ip 를 보고 routing table 을 참조해서 목적지 방향쪽 interface 를 DATA 를 전송

+목적지까지 책임지는것이 아니라 다음 Router 까지만 책임을 진다
 =>모든 router 가 모든 network 정보를 routing table 에 보유 해야 한다



## routing-table
routing table 을 참조

1>routing table 에 정보가 있어야만 전송이 가능 
    없으면 불가능 => routing table 을 완성

2>경로 검색,경로 선출,경로 유지 를 한다


경로 검색,경로 선출,경로 유지 를 관리자가 일일이 설정하는 것은 static routing protocol 이다

경로 검색,경로 선출,경로 유지 를 router 안에서 routing protocol 이 알아서 하는 것은
Dynamic routing protocol 이다



경로 선출

1>롱기스트 매치룰 : 목적지 ip 에 가장 길게 일치하는 경로가 선출
2>상황에 따라서 

-다수의 routing protocol 이 있을때(다수의 AD 값이 있을때) AD(신뢰도)값이 가장 작은 경로가 선출
 =>dynamic routing protocol 이 여러개일 경우는 거의 없다
 =>dynamic routing protocol 을 주로 쓰고 static 을 백업으로 쓰는 경우가 있다 
 =>routing protocol 의 AD 값은 변경할수 있다 

-동일한 routing protocol 이 있을때(동일한 AD 값이 있을때)metric(경로값)값이 가장 작은 경로가 선출
 =>dynamic routing protocol 은 metric 변경할 수 있다



  routing table 을 완성

1>interface 설정
    interface 설정을 했을때 routing table 에 등록이 되려면 2가지 조건이 있다
    - ip 대역대가 있어야 한다
    - L2 까지 up이 되어있어야 한다


interface 설정을 완성해서 routing table 에 등록


=> router 에 직접 연결된 network (directly conneted) 만 등록이 된다
     즉 routing table 이 전체적으로 완성이 되질 않는다 


routing table 을 전체적으로 완성 시켜주기 위해서  routing protocol 을 구동 시켜준다


## routing-protocol
 Routing protocol 의 종류 


## static  
-Static : 내가 모르는 네트워크 네임을 관리자가 일일이 설정 (남의 이름 물어보기)

ex>ip route 192.168.1.0 255.255.255.224  13.13.12.2


-Dynamic

  -IGP : AS 안에서 빨리빨리가 목적 : 내 네트워크를 관리자가 설정해주면 알아서 동적으로 전파 (자기 소개하기) interior gateway protocol
  rip igrp ospf is-is
  
    -distance vector  : Ripv1 , Ripv2

ripv1 

router rip
v 1
net 192.168.1.0
net 172.16.0.0
net 13.0.0.0

ripv2

router rip
v 2
no au
net 192.168.1.0
net 172.16.0.0
net 13.0.0.0


    -advance distance vector  : EIGRP


eigrp 

router eigrp 100
no au
net 192.168.1.0
net 172.16.0.0
net 13.0.0.0

or

router eigrp 100
no au
net 192.168.1.1 0.0.0.0
net 13.13.12.1 0.0.0.0
net 172.16.1.1 0.0.0.0


    -link state  : OSPF  , IS-IS


OSPF

router ospf 1
net 192.168.1.1 0.0.0.0 a 0
net 13.13.12.1 0.0.0.0   a 0
net 172.16.1.1 0.0.0.0   a 0

or

int s 1/0
ip ospf 1 area 0

int f 0/1
ip ospf 1 area 1


  -EGP: AS 와 AS 간에 많이 많이 
Path Vector (BGPv4) : routing table 에 있는 정보를 관리자가 설정해서 전파할수 있다 (우리 반 소개하기)

  => routing table 을 완성




ACL (Access-List)

-필터링 기능(Permit:허용    Deny:차단)
-방화벽과 같은 기능   
-QOS,VPN,PBR 기능의 구성 요소
-NAT,PAT 기능의 구성 요소



   ACL 구성 방법

1. 하향식 계산 : 설정을 하면 모두 마지막에 더해짐 

-자주 접속하는 것을 먼저 설정

A
B
C
D
E

C 가 왔을 경우 : A 확인하고 일치하지 않으니까 B 확인하고 일치하지 않으니까  C 확인하고 일치하니까 동작

E가 왔을 경우 : A 확인하고 일치하지 않으니까 B 확인하고 일치하지 않으니까  C  확인하고 일치하지 않으니까  D 확인하고 일치하지 않으니까  E 확인하고 일치하니까 동작

A 가 왔을 경우 : A 확인하고 일치하니까 동작

그러니까 자주 접속하는 것을 먼저 설정하는것이 좋다  => 주관적이다 => 상황봐서 진행



- host-id 가 좀더 좁은 범위의 것을 먼저 설정 

잘못된 설정 예제

172.16.0.0 /16  Deny 
172.16.1.0 /24  Permit

172.16.2.1  =>  Deny
172.16.1.1  =>  Deny

옳은  설정 예제

172.16.1.0 /24  Permit
172.16.0.0 /16  Deny 

172.16.2.1  =>  Deny
172.16.1.1  =>  Permit

=> 설정 순서가 상관이 있다


2.ACL은 임의의 줄과 줄사이것을 지우거나 수정할수 없다  즉 부분수정과 부분삭제가 불가능 
  단 named 는 가능 하다

=> 설정 순서가 상관이 있다


3.ACL 은 설정하면 무조건 마지막에 나머지는 deny 하겠다라고 선언된다
   나머지는 deny 하겠다를 상쇄시켜주고 싶으면 나머지는 permit 하겠다라고 설정을 해줘야 한다


4.ACL 을 설정할때는 처음부터 차례대로 빠짐없이 전부 설정해줘야 한다 
 (백업 권장)(구성할때 장비에 바로 설정하지 않고 메모장에 먼저 설정하고 
  계산하고  검사하고 검수받고 천천히 설정 진행을 하는편이다)



ACL 종류

Standard : Source


access-list[1~99][Permit or Deny][Source][Source.Wildcardmask]

access-list 10 deny 192.168.1.0 0.0.0.255
access-list 10 permit any 

Extended : Source ,Destination ,Protocol    ,Port,Keyword


access-list[100~199][Permit or Deny][Protocol][Source][Source.Wildcardmask][Source.Port][Destination][Destination.Wildcardmask][Destination.port][Keyword]


access-list 100 deny ip 192.168.1.0 0.0.0.255 13.13.10.0 0.0.0.255
access-list 100 permit ip any any



Day7 오전
ACL 적용

적용을 해준 곳에서만 ACL 이 동작을 한다

[참고]
ACL 설정은 목적지에 가장 가까운 router 에서 설정하는것이 좋다


13.13.10.0 /24 은 13.13.20.0 /24  로 접근하지 못하게 하여라  
 
standard

access-list 10 deny 13.13.10.0 0.0.0.255
access-list 10 permit any

적용

int s 1/1
ip access-group 10 in

or

int f 0/0
ip access-group 10 out

extended

access-list 100 deny ip 13.13.10.0 0.0.0.255 13.13.20.0 0.0.0.255
access-list 100 permit ip any any

적용

int s 1/1
ip access-group 100 in

or

int f 0/0
ip access-group 100 out



[named]
부분 수정 및 부분 삭제가 가능 

ip access-list extended  AAA
[Permit or Deny][Protocol][Source][Source.Wildcardmask][Source.Port][Destination][Destination.Wildcardmask][Destination.port][Keyword]


ex>

ip access-list extended AAA
deny ip 192.168.1.0 0.0.0.255 ho 1.1.1.1
  
permit ip any any


적용

int s 1/1
ip access-group AAA in

or

int f 0/0
ip access-group AAA out

[참고]
sequence 숫자 정리해주는 방법 : ip access-list resequence AAA 10 10 


1.13.13.20.0/24 는 13.13.10.0/24 로 텔넷은되고 핑은 안되게 하여라 
2.13.13.30.0/24 는 13.13.10.0/24 로 텔넷은안되고 핑은 되게 하여라



ip access-list extended AAA
deny icmp 13.13.20.0 0.0.0.255 13.13.10.0 0.0.0.255
deny tcp 13.13.30.0 0.0.0.255 13.13.10.0 0.0.0.255 eq telnet
permit ip any any


적용


int s 1/0
ip access-group AAA in

or

1.13.13.20.0/24 는 13.13.10.0/24 로 텔넷은되고 핑은 안되게 하여라 
2.13.13.30.0/24 는 13.13.10.0/24 로 텔넷은안되고 핑은 되게 하여라

ip access-list extended AAA
permit tcp  13.13.20.0 0.0.0.255 13.13.10.0 0.0.0.255 eq 23
permit icmp 13.13.30.0 0.0.0.255 13.13.10.0 0.0.0.255
permit ospf any any

적용


int s 1/0
ip access-group AAA in





Day7 1:41 PM

  NAT 

inside local address 를 inside global address 로 변환
=>내부의 ip 를 외부의 ip 로 변환
=>내부의 사설 ip 를 외부의 공인 ip 로 변환
=>보안성이 좋아진다. ip 고갈문제를 해결



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



-dynamic


  -pool 을 이용하는 방법

access-list 10 permit ho 10.1.1.1
ip nat pool AAA 172.16.1.1 172.16.1.1 prefix-length 24
ip nat inside source list 10 pool AAA overload


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




2>NAT 이론


-static  :  1:1  지정 방식 (설정을 하면 자동적으로 NAT table 이 생성이 되고 삭제(clear ip nat tr *)가 불가능하고 유지시간도 없다)
          

-dynamic :한번 변환이 되어야 NAT table 이 생성이 되고 삭제(clear ip nat tr *)가 가능하고 유지시간이 있다

  -NAT:단순 변환 , 1:1 방식 , 유지 시간 1일
  -PAT: 확장 변환,  1:다수 방식 , 유지 시간 1분 (overload)


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


DISCOVER : Client가 Server 에게 ip를 요청(client의 MAC주소 포함) Server 가 중복확인(unicast[ICMP])

OFFER : Server 가 Client 에게 ip 를 할당 (client의 MAC이 목적지)

REQUEST :ip 사용에 대한 최종확인(client의 MAC포함) => DHCP 서버가 2대이상일수 있어서

ACK : 선택되지 않은 Server 는 ip를 회수 
     선택된 server는 나머지 정보(subnetmask,default gateway,DNS 정보등등)를 할당 승인


                             			                    출발지 ip        목적지 ip		
Client     68 번 포트를 사용   C ------------> S     DISCOVER        0.0.0.0        255.255.255.255
Server    67 번 포트를 사용   S ------------> C     OFFER            Server ' ip     255.255.255.255
Client     68 번 포트를 사용   C ------------> S     REQUEST         0.0.0.0        255.255.255.255
Server    67 번 포트를 사용   S ------------> C     ACK               Server ' ip     255.255.255.255



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



[참고]
'ip helper-address' 기능

-수신한 브로드케스트를 유니케스트로 변환시켜주는 기능




Router 는  routing 

routing 

router 가 ip 헤더안에 있는 목적지 ip를 보고 routing table 을 참조해서 
목적지가 있는 방향쪽 interface 로 packet 전송

routing table 을 참조 => routing table 에 있어야만 전송이 가능 없으면 전송이 불가능 

=> 기본적으로 routing table 이 없다 =>routing table 을 완성 => 관리자가 설정을 해서 



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



4.VTP(Vlan Trunk Protocol) sh vtp status

vlan database 정보를 trunk port 를 통해서만 교환하는 protocol
(옵션:설정을 한다면 가장 먼저 설정하는것이 좋다: vlan 구성 용이,vlan 관리 용이,trunk설정 완성을 확인)


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


기본 mode 는 Server

설정

vtp mode server
vtp mode client
vtp mode transparent



Configuration Revision 은 처음엔 0 이고 VLAN 정보가 변경될 때 마다 ‘1’ 카운트씩 증가된다 수신한 VTP 메시지의 ‘VTP Configuration Revision’ 값이 더 높을 경우에는 자신의 VLAN 정보를 상대방 스위치의 VLAN 정보로 일치시켜 공유한다. 만약, 수신한 VTP 메시지의 ‘VTP Configuration Revision’ 값이 자신과 동일하다면 VTP 메시지를 무시하며, 자신의 ‘VTP Configuration Revision’ 값이 더 높을 경우에는 상대방 스위치에게 자신의 VTP 메시지를 광고한다.

트랜스패런트 모드는 VLAN 정보가 변경되어도 ‘VTP Configuration Revision’ 값이 항상 ‘0’으로 고정된다. 그렇기 때문에 ‘VTP Configuration Revision’ 값을 초기화할때에도 사용된다






5.inter-vlan 

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




Network 구축의 핵심

-확장성
-이중화
  -백업
  -로드 분산


Router 간의 이중화는 문제가 없다
 
Switch 간의 이중화는 문제가 발생 (bridging Loop : 브릿징 루프)가 발생


 Bridging Loop 종류
 -broadcast storm
 -copy unicast frame (유니케스트 프레임을 복제)
 -MAC Flapping (MAC 주소 테이블 불안정화)


STP
스위치간의 물리적으로 이중화 되어 있는 구간을 논리적으로 block 시켜주는 것
=> siwtch 간의 이중화 구현이 가능 하다
=> 이중화 구간이 X 개면 block 도 X 개여야 한다



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

## 5부 라우팅 개요

Router 가 사용하는 스위칭 방식
=> routing table 참조 여부

-Process switching : DATA 를 전송할때마다 매번 routing table 을 참조하는 방식 

-Fast switching :처음에만 routing table 을 참조하면서 자신의 캐시table 에 복제하고 이후에는 캐시 table 을 참조해서 DATA  전송 --< 목적지 ip 주소에 따라서>

-CEF : routing table 이 완성이 될때 자신의 CEF table 에 복제를 하고 CEF table 을 참조해서 DATA 를 전송 
         즉 rouing table 을 한번도 참조하지 않는다
         Cisco express forwarding <출발지 목적ip 주소에 따라서 경로가 달라진다.  ip loading share per packet>

routing table 을 매번 참조하든 아니든 routing table 에 있어야만 복제를 할수가 있다 
즉 routing table 에 정보가 있어야 통신이 가능하다 없으면 통신이 불가능

do sh ip domain

[참고]
로드 분산을 하는 경우의 차이

-Process switching : 매번 차례대로 진행을한다
-Fast switching :목적지 ip 주소에 따라서 경로가 달라진다
-CEF : 출발지 ip , 목적지 ip 주소에 따라서 경로가 달라진다 

+ CEF : ip load-sharing per-packet 을 로드 분산할 interface 설정을 하면 패킷별로 로드 분산이 된다  

### Dynamic
AS (autonomous system)

==> 지역단위 (대학, 통신사 지사)

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


  ## 6부 RIP

  3:14 PM
  
### distance vector의 특징
 distance vector

주기적으로 인접한 router 에게만 routing table 전체를  update 한다

update 를 위한 대역폭 소비량이 많다
update 를 위한 CPU 소모율이 많다 
=> 장비 소모량이 많다

구조가 간단하다
확장성이 떨어진다
변화에 적응이 느리다
알고리즘상 루프가 발생을 한다
(루프 방지법:Split-Horizon : 수신한 정보를 수신한 interface 로 다시 전송하지 않는다)  eigf


###
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

- 9.<u>균등 로드 분산만 지원</u> (기본 4개 ~ 최대 16개) 범위 : 1 ~ 16 까지 조절이 가능 

10.metric = hop  count = Router 경유 수(범위:1 ~ 15) 16이면 limit 라고 해서 장애 발생으로 인식

11. ripv1 필수 설정

ripv1 은  classful 로 동작 , 설정은 classful 하게 설정

** [주의]동작과 설정은 별개

172.16.1.0 /24
13.13.10.0 /24
13.13.12.0 /24

router rip 
v 1
net 172.16.0.0
net 13.0.0.0

router ?
router rip
network (net)
서브넷 무시
1cass
router rip
net 172.16.0.0
net 13.0.0.0


###
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



### Ripv2  옵션 설정

1> triggered  update 설정 (WAN 구간 P2P 구간만 지원)


triggered  update 를 할 구간에 연결된 모든 interface 에서 설정

R1
int s 1/0
ip rip triggered

R2
int s 1/1
ip rip tr

triggered  update 를 설정을 하면 주기적인 update 를 하지 않는다
변화가 생겼을때만 update 를 해준다 (multi cast)



2>해시함수를 이용한 MD5 인증 설정 (수학적 계산법, 무결점 증명)


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



보안

기밀성
data  유출방지

암호화: 복호화가 가능
암호화 알고리즘. 키값
[1234] => [!@#$] ==> [1234]

무결성
data 변조를 방지

인증: 복호화가 블가능
인증 알고리즘
키값
!@#$ --해쉬 값
 [!@#$][1234]

 router rip
 v 2
 net 172.16.0.0
 net 13.0.0.0
 no auto summary (no au)

Day5    12:21 PM
router - id (eigrp, ospf, bgv4) 
Router 를 구분하는 식별자 (IPv4 주소 형식으로만 진행*IPv6 에서도 동일하다)

Router - id 선출 기준

1.설정

router eigrp 100
eigrp router-id 1.1.1.1

2.loopback interface 의 ip 중에서 숫자가 가장 큰 ip 가 router-id 로 선출

3.물리적인 interface 의 ip 중에서 숫자가 가장 큰 ip 가 router-id 로 선출

(p236 ex-24-14)

eigrp torpology table analysis

(동영상 참고) 12:46 PM

[참고] 12:50 PM
비균등 로드 분산을 하려면 2가지의 조건이 만족 되어야 한다

1>variance 값을 이용해서 최적 경로의 metric 보다 비균등 로드 분산 하려는 경로의 metric 을 작게 만들어 준다

2>최적 경로의 FD 보다 작은 AD 값을 가지고 있어야 한다(후속 경로)
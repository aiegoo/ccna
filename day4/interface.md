## interface setting

> routing table checkup list
> do sh ip router
> do ip ip address
> ping이 안되는 경우 t/s실시
> do sh ip int brief --> 각각의 장비 콘솔에서 실시
> int s 1/1
> ip add ....content1
> do p   ping test

interface 구성 개념을 갖고, 라우팅 프로토콜 및 옵션의 잘못된 점을 찾아내고, 이를 ts 할 수 있는 능력

12:13 PM
hold time: 연결하고 세션 데이타를 생성해내는 시간
장비의 이름을 주는 것은 옵션이기는 하지만, 당연히 해야 함.

> do p   내테이블에 있고 상대방도 있으면 성공함.content1
> 네트워크 아이디의 갯수가 각각 7개씩의 라우팅테이블이 나와야 함. 
> 
### routing-table

[routing table 을 참조

1>routing table 에 정보가 있어야만 전송이 가능 
    없으면 불가능 => routing table 을 완성

2>경로 검색,경로 선출,경로 유지 를 한다


경로 검색,경로 선출,경로 유지 를 관리자가 일일이 설정하는 것은 static routing protocol 이다

경로 검색,경로 선출,경로 유지 를 router 안에서 routing protocol 이 알아서 하는 것은
Dynamic routing protocol 이다
] ()

12:30 PM routing protocol types 
RIPv1만 classful임으로 서브넷마스크를 요하지 않고 나머지는 classless임.
> dynamic (IGP)
> eigrp
> 라우팅 프로토콜은 인터페이스 설정이 제데로 되었을때 가능함.
> 본인외 남은 네트워크 설정을 하는 것이  statick setting 이라고 함.

-Static : 내가 모르는 네트워크 네임을 관리자가 일일이 설정 (남의 이름 물어보기)


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
> ip route [내가 모르는 네트워크'네임][netmask][next hop'ip]
> ip route [내가 모르는 네트워크 ' 네임][netmask][발신 interface 의 이름]

R1 1, 0 10 13

1:08 PM (사진 참고)
R1
ip route 13.13.13.0 255.255.255.0 13.13.12.2
ip route 13.13.23.0 255.255.255.0 13.13.12.2
ip route 13.13.30.0 255.255.255.0 13.13.12.2
ip route 13.13.3.0 255.255.255.0 13.13.12.2

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


### 경로검색
2> 경로 검색 => 경로 선출 => 경로 유지  --> 관리자가 하느 경우 static, 라우터가 하는 경우 dynamic

1.롱기스트 매치룰 : 목적지 ip 에 가장 길게 일치하는 경로가 선출
목적지 ip : 172.16.1.1  -- 32비트

172.16.1.0 /24  경로 선출 (매칭되는 아이피주소가 길어서 임)
172.16.0.0 /16

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

실습
do sh ip route
do sh run --> static에서 물어 보는 과정
ping test로 완성함


## 정적 기본 경로

ip route 0.0.0.0 0.0.0.0 13.13.12.2
S* static default 0.0.0.0/0

-default  static 

설정

ip route 0.0.0.0 0.0.0.0 [next hop'ip]

or

ip route 0.0.0.0 0.0.0.0 [발신 interface 의 이름]



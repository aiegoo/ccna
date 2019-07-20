day 6 4:50 PM
28장
## ACL (Access-List)

-필터링 기능(Permit:허용    Deny:차단)
-방화벽과 같은 기능   
-QOS,VPN,PBR 기능의 구성 요소 public base router
-NAT,PAT 기능의 구성 요소 (주소변환)


  ACL 구성 방법

1. 하향식 계산 : 설정을 하면 모두 마지막에 더해짐 (설정순서 상관있음, 징집 기준 예)

-자주 접속하는 것을 먼저 설정


- host-id 가 좀더 좁은 범위의 것을 먼저 설정 


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
protocol -> ip icp pcp udp eigp ospf
source port 잘 안함 -- source port가 랜덤이기때문에


access-list 100 deny ip 192.168.1.0 0.0.0.255 13.13.10.0 0.0.0.255
access-list 100 permit ip any any


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

목적지에 가까운 라우터에 설정한다. ()

12:01 PM Day7
[named]
부분 수정 및 부분 삭제가 가능 

ip access-list extended  AAA
[Permit or Deny][Protocol][Source][Source.Wildcardmask][Source.Port][Destination][Destination.Wildcardmask][Destination.port][Keyword]

ip access list resequence (re)
ip access-list resequence AAA
sh ip

12:22 PM 9 녹음파일 --일부만 했음
12:33 PM  까페 문제 풀이 녹화 끝

연습문제 https://cafe.naver.com/itguild/147
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

 

 

2.ospf 설정을 해준다.단 각각의 라우터 아이디는 각각의 라우터 번호로 해준다..ex> R1 은 1.1.1.1

 

R1

 

router ospf 1

router-id 1.1.1.1

net 172.16.1.0 0.0.0.255 area 0

net 13.13.10.0 0.0.0.255 area 0

net 13.13.12.0 0.0.0.255 area 0

 

R2

 

router ospf 1

router-id 2.2.2.2

net 13.13.12.0 0.0.0.255 area 0

net 13.13.20.0 0.0.0.255 area 0

net 13.13.23.0 0.0.0.255 area 0

 

R3

 

router ospf 1

router-id 3.3.3.3

net 13.13.23.0 0.0.0.255 area 0

net 13.13.30.0 0.0.0.255 area 0

net 172.16.3.0 0.0.0.255 area 0

 

 

3.sh ip route 로 본래의 서브넷 마스크로 전파를 하였는지 확인한다.안되었다면 제대로 전파를 해줄수 있게 설정한다.

 

 

R1

 

int lo 172

ip ospf net point-to-p

 

R3

 

int lo 172

ip ospf net point-to-p





R1 에 텔넷 설정

 

line v 0 4

pass cisco

login

 

설정을 다한 이후에

 

13.13.20.0/24 는 13.13.10.0/24 로 텔넷도되고 핑도 되는지 확인하여라

13.13.30.0/24 는 13.13.10.0/24 로 텔넷도되고 핑도 되는지 확인하여라

 

 

확인한 이후에 ACL 문제를 푼다

 

1.13.13.20.0/24 는 13.13.10.0/24 로 텔넷은되고 핑은 안되게 하여라
2.13.13.30.0/24 는 13.13.10.0/24 로 텔넷은안되고 핑은 되게 하여라

 

적용
int s 1/0
ip access-group 100 in

 

확인방법

 

R2
ping 13.13.10.1 source 13.13.20.1
telnet 13.13.10.1 /source-interface f0/0


R3
ping 13.13.10.1 source 13.13.30.1
telnet 13.13.10.1 /source-interface f0/0
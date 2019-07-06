## 14장 라우터 패스워드 관련 설정

password 설정 (옵션 설정 : 장비 접속에 대한 보안이 좋아진다)

#### enable
1>enable (주의점:password 의 대소문자 구분되고 스페이스 바도 입력이 된다)

- secret : 암호화 , 우선 순위가 높다    설정  : enable secret cisco
- 일반   :  평문 , 동일하면 안된다        설정 :  enable pass soldesk

Router>en
password:

IP/Pass 덮어씌우기가 기본임

#### line
2>line

login 유무에 따라서 password 입력 유무가 정해짐 

|    |    |    |
|:---|:---|:---|
|    |    |    |
|    |    |    |

line c 0
pass cisco
login

line a 0
pass cisco
login

line v 0 4
pass cisco
login

Router con0 is now available

Press RETURN to get started.

User Access Verification

Password:cisco 
Router>

login 유무에 따라서 password 입력 유무가 정해짐 
password 입력 유무에 따라서 접속 유무가 정해짐 


line v 0 4
pass cisco
login



R1#telnet 13.13.12.2
Trying 13.13.12.2 ... Open

User Access Verification

Password: cisco

## interface 설정
ccna 기본설정

loopback 관리목적
이더넷
시리얼
위와 같은 순서로 하는게 편리함. 의무는 아님.

loopback interface : 가상 interface로 실제 DATA를 송수신 불가능 하다

-관리 목적: ping test , telnet or SSH 같은 원격 접속 가능 ,  IOS upgrade or IOS backup 등을 할때
ip 가 필요하다 물리적인 interface 는 변경이나 피해를 볼수 있지만 loopback interface 는 물리적으로 
피해를 볼일이 없다 그래서 관리 목적으로  loopback interface 를 사용하자

### 인터페이스 연습 
Loopback의 인터페이스 이름은 상관이 없다.
h0 r1

ip lo 172
ip add 172.16.1.1/24
no shutdown은 구지 할 필요는 없다. 자동으로 up 됨


int f0/0
ip add 13.13.10.1/24
no shut

int s 1/0
ip add 13.13.12.1/24
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

### 기타 옵션 설정

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

까페.. itguilde ccna>두번째 항목을 따라 해보기


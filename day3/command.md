제3부 p116
<pre>
RAM : 설정을 하면 자동적으로 RAM 에 저장이 되고 장비는 RAM 에 있는 내용대로 동작을 한다  휘발성 메모리 : 재부팅을 하면 무조건 삭제가 된다

NVRAM : 명령어를 입력해야만 저장이 되고 명령어를 입력해야만 삭제가 된다 
           비 휘발성 메모리 : 재부팅으로 삭제가 되지 않는다  (save file 로 생각하면 된다)
           0x2102  vs 0x2142 (x뒤 숫자는 16진수)

NVRAM  참조 여부

config-register 값

0x2102 : NVRAM 을 로드 하는 값
0x2142 : NVRAM 을 로드 하지 않는 값

</pre>

### Cisco router 2800 series
https://www.andovercg.com/datasheets/cisco-2800-series-router.pdf

data, voice and video intergrated services router

## cisco ios 명령어


mode: 생김새, 하는 일

router> 사용자모드
router>en

router# privilege mode, 관리자 모드

### 하는 일
<pre>
저장(copy run start --> ram의 내용을 nvram에 저장한다는 뜻) , 삭제(erase start) , 재부팅(reload) ,ping test 및 traceroute, telnet 및 ssh 접속 , clear

show : 정적 분석.... 명령후 확인하는 데 사용. 10개정도 암기
debug: 동적 분석, 시간이나 이벤트에 따라서.
show  : 정적 정보 확인
          - 그때 그당시에 그 상황에 대해서만 정보 확인이 가능 
             그래서 변화가 생기면 계속 확인을 해야 한다 

debug : 동적 정보 확인
        - 명령어에 따라 다르지만 시간 혹은 변화에 따른 정보 확인을 지속적으로 확인이  가능 
            그래서 필요하면 확인하고 필요 없으면 종료

시스코는 기본적으로 내용을 삭제한다거나 동작을 멈추거나 아니면 동작은 반대로 할 경우에 똑같은 상황(mode , 명령어) 앞에 no 를 쓰면 된다 ex) no shutdown, no debug ip lib. privilege mode에서 

clear : process를 다시 시작하는 명령어

Router#conf t --> configure terminal
Router(config)# configuration global mode, 설정모드
전반적인 설정 및 상세 설정 모드로의 접근

Router(config)#router ospf 1

exit --> 전단계로 이동함

Router>en
Router#conf t
Router(config)#line c 0
Router(config-line)#exit
Router(config)#line c 0
Router(config-line)#end  or Ctrl+z
Router#
</pre>

(위의 copy run start 방법의 이용 예)

### 패스워드 리셋 방법
(녹음 화일 확인 12:41 PM)
기기 전원을 온/오프한 후

0x1242 이후

copy run start (덮어쓰기 하는 방법)

reload


## 실습
1:11 PM  녹음화일 (이사간에 중지했음)

en level 0 -15까지 있그 15는 관리자 모드

1:15 PM (녹음화일) 1:17 PM

## 정보확인

mac arp 테이블은 자동 완성되나 routeing table은 임의 설정되어야 함.content1

sh ip route : IPv4 unicast routing table 의 정보 확인

sh ip int bri : 장비의 모든 interface 의  간략한 정보 확인

> ip-address (layer 3)
> status (layer 1)
> protocol (layer2)

--> ping이 된다는 것은 3계층까지 문제가 없다는 것임.
administively down --> no shutdown 해주어야 함.

### 씨시코 설정 3
일반적으로 설정 순서가 상관이 없다.

down/down의 경우
layer 1의 문제

up/down의 경우
clock rate
Hldc ppp 설정이 서로 다른 경우(wan)

up/up
문제가 없는 경우


### sh run
sh  run : RAM 상에 설정된 전체적인 정보 확인
sh start : NVRAM 상에 저장된 전체적인 정보 확인

do 명령어는 다른 단계의 명령어를 사용할 수 있게 한다.

hostname

interface

line -- 장비에 접속할 수 있는 방법
con
aux
vty - virtual terminal --> ssh, telnet

line con 0  -- 1명
line aux 0  -- 1명
line vty 0 4 - 5명

RAM 을 NVRAM 에 저장하는 명령어 : copy run start  , wr me  , wr


sh cdp nei [detail]:

sh cdp nei [detail] : 상대방 장비 정보[상세하게]를 확인 , L2 까지 up이 되어있어야 한다
sh int [s1/0]:[해당] interface 의 전체 정보 확인
sh ip int [s1/0] :ip가 동작하는 [해당]interface 의 정보 확인

IOS upgrade , backup 을 할때
-IOS 버전 정보 확인: sh ver
-Flash memory 정보  확인 : sh fla

재부팅 : reload

### 설정
셋업모드

시스코 기본 --
설정은 기본적으로 덮어씌우기 안된다


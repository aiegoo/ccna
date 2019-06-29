## osi 계층 참조 모델 open system interconnection
![osi model](osi-model.jpeg)

### 네트워크 설계를 위한 기준을 제공
호환성 제공
T/S용이 (장애복구)

예)
통신이 안될 경우
ping (ICMP protocol ) 3계층 프로토콜임 - (네트워크계층)

1계층 - 물리적 (선이 빠짐)
2계층 - 데이타 링크

-----

### 상위계층 - 데이터를 생성,  주로 OS에서 담당
- 7계층 - application : 사용자를 위한 계층
- 6 - presentation : 장비간의 커뮤니캐이션 (암호화, 압축)
- 5 - session: OS간의 논리적 연결 (다양한 옵션 결정) => PDU


하위계층 - 데이타를 전송(주소: 출발지 목적지)
- 4 - transport[TCP or UDP][DATA] - Segment, port (16bit)
[]헤더를 붙임 - 이렇게 하는것을 encapsulation 
TCP UDP
TCP -- http에 붙으므로 주로 사용
연결지향 서비스 = handshaking (연결이우선)
(카메라)
신뢰적인 서비스 ==> flow control. eror control & error correction(재전송 checksum), congestion control(전송율 제어) 묶어서 한번에 sliding window기법 
> tcp flag
sync: 연결을 개시
ack: 승인
fin: 정상적인 종료

UDP 
비연결 지향 서비스 (best effort)
8byte로 용량이 적음
실시간 - 전화, 웹비나, 멀티미디어 환경

- 3 - network[IP][TCP or UDP][DATA] (ip address) Packet IPv4, 32bit, 10진수, 논리적인 주소 4294967296 (2sup32) 라우터
IP: BE방식
ICMP: internet control message request(8) ==> reply(0) 핑을 이용
IGMP
**ARP**: lan구간에서 중요. IP를 이용해서 MAC주소를 알아 온다.
- 2 - data link [Ethernet][IP][TCP or UDP][DATA] frame, mac address, 16, 48bit
MAC주소는 앞 oui-24라고해서 회사이름이록 뒤에는 고유번호가 붙음. 스위치
enternet
wan: hdlc ppp frame-relay

- 1 - physical: 전기적인 신호로 변환 및 출력, bit, hub


----------- 4:08 PM

ethernet data 전송유형
half duplex: 무전기
full duplex: 전화기

허브 (카메라)
CSMA/CD
carrier sense multiple access collision detection
backoff

L1 hub
L2 switch: CD을 나눠준다. full duplex, 같은 bd broadcast domain 안에 있다
L3 router: 물리적으로

라우팅 테이블을 참조한다는 것의 의미
테이블에 내용이 있은면 전송이 가능
없으면 전송 불가능

-- 모든 라우터가 다른 모든 라우터의 정보를 다가지고 있어야 한다.
수업의 예제에서는 라우팅테이블이 4가지가 나와야 한다.

-- 2계층에서는 네트워크 상황에 따라 바뀌는 반면 3계층에서는 바뀌지 않는다.
통신할때 2계층은 계속 바뀌는 반면.. 3계층은 바뀌지 않고 하나의 수치가 계속 이동한다.

라우팅테이블은 설정을 통해서 만들어지고
ARP테이블은 기본적으로 없음.
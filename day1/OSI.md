## osi 계층 참조 모델 open system interconnection


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
TCP
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
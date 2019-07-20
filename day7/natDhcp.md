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

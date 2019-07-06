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
| line c 0
pass cisco
login   |  line c 0
pass cisco
login  | line a 0
pass cisco
login   |
| line v 0 4
pass cisco
login   |    |    |


Router con0 is now available

Press RETURN to get started.

User Access Verification

Password:cisco 
Router>
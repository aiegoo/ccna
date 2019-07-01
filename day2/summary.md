<!-- vscode-markdown-toc -->
* 1. [Tasks](#Tasks)
* 2. [EVE 설치방법 step1 2](#EVEstep12)
* 3. [step3](#step3)
* 4. [step 4](#step4)
	* 4.1. [가상머쉰 스타트!!!!](#)
* 5. [step 5](#step5)
* 6. [step 6](#step6)
* 7. [step 7](#step7)
* 8. [step 8](#step8)
* 9. [step 9](#step9)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

from diary
- MEMO: ram nvram을 구분하여 공부하자. 설정하면 자동저장되는것이 램. 휘발성 메모리
- nvram 명령어를 입력해야만 저장되고 명령어로 삭제 됨. 비휘발성 메모리임.

- NOTE: [cisco util](cisco_util.md)

[crt 5.0](https://cezacx2.tistory.com/522)
[dyna gen](https://dynagen.com/sites/default/files/Support%20Files/MAN-0095R1.1,%20DYNAGEN%20Configurator%20Manual.pdf)
[packet tracer 7](https://www.itechtics.com/packet-tracer-download/)


# Saturday, July 6, 2019
- MEMO:  todo winPcap.org에서 다운로드한후 실행해서 설치함, 이후 다시 다이나밉 실행함
- MEMO: GNS EVE, EVE가 고급 이상적임

##  1. <a name='Tasks'></a>Tasks
- [ ] TASK: start R1 R2 R3
- [ ] TASK: dynammips 폴더에서 tmp 내용 삭제하고,  다이나밉스서버 실행하고 최소화한수 ccna를 클랙함
- [ ] TASK: secure crt, putty hyperterminal -- CRT로 랩을 진행
- [ ] TASK: dynamips dynagen.org - 애뮬. VM과 비슷 1인 3라우터 형태로 랩을 구성함
- [ ] TASK: routing event design and equipment

##  2. <a name='EVEstep12'></a>EVE 설치방법 step1 2

>http://blog.naver.com/PostView.nhn?blogId=jga0674&logNo=221030110935
![step 1 even-ng.net eve-ng..eve..OVA -MEGA mirror](attatched/1.png)
![step 1 download button](attatched/1-1.png)
![step 2 download widnows client](attatched/2.png)
![step 2 download widnows client](attatched/2-1.png)
<br>`all the necessary files have so far been downloaded`

##  3. <a name='step3'></a>step3

>Step3 VMware에 OVA 파일을 가상 피씨로 등록 - VMware 12 pro
![VMware 12 pro setup 1](attatched/3.png)
![VMware 12 pro setup 2](attatched/3-1.png)
![VMware 12 pro setup 3](attatched/3-2.png)

##  4. <a name='step4'></a>step 4

`<Step4 설정하기>`
![Device Processor setting 1](attatched/4.png)
![Device Processor setting 2](attatched/4-1.png)
![Device Processor setting 3](attatched/4-2.png)

###  4.1. <a name=''></a>가상머쉰 스타트!!!!

+     steps
      - default user/pw = root/eve
      - root pw setting box
      - hostname setting
      - domain name setting
      - dhcp/static ip setting
>go to Edit>virtual network editor
![](attatched/networkEditor.png)

>Gateway DNS 설정
![](attatched/defaultGateway.png)
![](attatched/gateway.png)
![](attatched/dnsserver.png)

> 가상 머쉰이 재부팅된다.
-----

##  5. <a name='step5'></a>step 5

>Step5 WinSCP installation and setup
`[link]`: https://winscp.net/eng/download.php
![](attatched/winscp.png)

##  6. <a name='step6'></a>step 6

>Step6 file transfer and settings
![](attatched/winscpFiletransfer.png)
![](attatched/winscpSetting.png)

##  7. <a name='step7'></a>step 7

>Step7 Client and terminal install and config
![](attatched/terminalClient.png)

##  8. <a name='step8'></a>step 8

>step8 Webbrowser login and adding additional equipment
![](attatched/webBrowserAdd.png)

##  9. <a name='step9'></a>step 9

>step9 expanding vm hd capacity and wireshark
![](attatched/expandHDwireshark.png)
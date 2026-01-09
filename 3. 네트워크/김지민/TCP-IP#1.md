# 캡슐화, 비캡슐화, PDU, OSI 7계층

#### TCP / IP TCP(Transmission Control Protocol) / IP(Internet Protocol) 의미, 인터넷에서 데이터를 전송할 때 가장 핵심적인 두 프로토콜이 바로 TCP와 IP
![](https://velog.velcdn.com/images/shypanda0119/post/6e879ab8-26f0-461c-b287-bc8bf7ac36ee/image.png)

### TCP/IP 4계층
#### 애플리케이션 계층(Application)이란?
우리가 사용하는 웹 브라우저, 이메일, 파일 전송 도구 같은 사용자 인터페이스(UI)를 가진 프로그램과 혼동하기 쉽지만, 그 프로그램이 네트워크와 통신할 수 있도록 도와주는 프로토콜이 모여있는 기능적인 계층
1. HTTP(HyperText Transfer Protocol) : 웹 페이지, 이미지, 동영상 등 웹 리소스를 요청/응답 ex) 브라우저에서 https://www.google.com 입력
2. SMTP(Simple Mail Transfer Protocol) : 이메일을 서버로 전송할 때 사용 ex) Gmail, Outlook이 메일을 보낼 때
3. FTP(File Transfer Protocol) : 파일 업로드 / 다운로드 ex) 서버에서 웹사이트 배포
4. SSH(Secure Shell) : 원격 로그인, 명령어 실행 ex) ssh user@ip로 서버 접속

#### 전송 계층(Transport)이란?
TCP, UDP가 대표적이며 애플리케이션 계층에서 받은 메시지를 기반으로 세그먼트(TCP) 또는 데이터그램(UDP)으로 데이터를 쪼개고 데이터가 오류없이 순서대로 전달되도록 도움을 주는 층

#### 인터넷 계층(Network)이란?
IP, ICMP, ARP가 대표적이며 한 노드에서 다른 노드로 전송 계층에서 받은 세그먼트 또는 데이터그램을 패킷화하여 목적지로 전송하는 역할

#### 링크 계층(Link)이란?
전선, 광섬유, 무선 등으로 데이터가 네트워크를 통해 물리적으로 전송되는 방식을 정의(데이터 링크 계층과 물리계층을 합친 계층)

### 캡슐화와 비캡슐화
#### 캡슐화(encapsulation)란?
송신자가 수신자에게 데이터를 보낼 때 상위 계층의 데이터를 하위 계층이 감싸면서 헤더(및 트레일러)를 붙이는 과정을 의미
1. 응용 계층 : 사용자가 이메일을 작성하고 전송 버튼을 누름
2. 전송 계층(TCP/UDP) : 응용 계층에서 받은 데이터를 "세그먼트(segment)"로 만들고, TCP 헤더를 붙임
3. 인터넷 계층(IP) : TCP 세그먼트를 받아 IP 주소가 담긴 IP 헤더를 붙여 "패킷(packet)"을 만듬
4. 데이터 링크 계층(Ethernet 등): IP 패킷에 MAC 주소 등의 정보가 담긴 프레임 헤더와 트레일러(FCS 등)를 붙여 "프레임(frame)"을 만듬
5. 물리 계층 : 프레임을 0과 1의 전기 신호나 광 신호로 변환하여 전송

#### 비캡술화(descapsulation)란?
수신자측에서는 이렇게 캡슐화된 데이터를 역순으로 제거하면서 응용계층까지 도달하는 것을 의미
![](https://velog.velcdn.com/images/shypanda0119/post/e850b405-3bba-402f-93ed-8d82d64107cd/image.png)

### PDU
#### PDU(protocol data unit)란?
TCP/IP 4계층을 기반으로 설명했을 때 각 계층의 데이터 단위를 의미
- 애플리케이션 계층 : 메시지
- 전송 계층 : 세그먼트(TCP, 연결형 데이터 조각), 데이터그램(UDP, 비연결형 데이터 조각)
- 인터넷 계층 : 패킷
- 데이터링크 계층 : 프레임(링크 계층, FCS 트레일러가 붙음)
- 물리 계층 : 비트 (링크 계층, 전기 신호 또는 광 신호)

### OSI 7계층
![](https://velog.velcdn.com/images/shypanda0119/post/da194f65-8b61-4d47-aa3f-3fceae7833b1/image.png)

#### 체크섬
데이터를 전송할 때 오류가 발생했는지 확인하기 위해 덧붙이는 추가 데이터 조각, "받은 데이터가 손상됐는지 아닌지"를판별하는 값을 말함 
![](https://velog.velcdn.com/images/shypanda0119/post/175d3039-6f44-43c5-89f8-f456b34e548b/image.png)

#### 1의 보수합
모든 데이터를 16비트 단위로 더한 후, 그 합의 1의 보수를 취해 체크섬으로 사용한다는 것 

#### CRC(Cyclic Redundancy Check, 순한 중복 검사)
원본 데이터에 0을 (다항식 차수)만큼 덧붙이고 해당 비트를 왼쪽에서 부터 차례대로 XOR 기반 이진 나눗셈을 수행





# MTU, MSS, PMTUD
### MTU(Maximum Transmission Unit)이란?
네트워크에 연결된 장치가 한번에 처리할 수 있는 최대 패킷의 크기

**패킷이 분할되지 않는 경우**
IPv6는 분할을 허용하지 않음. 패킷이 너무 크면 라우터가 폐기하고 Packet Too Big ICMPv6 메시지를 보냄

IPv4 헤더에는 flags라는 필드가 있는데 여기서 bit가 1이 되면 "Don't Fragment" 플래그가 활성화된다는 의미(이때 분할은 불가능)
![](https://velog.velcdn.com/images/shypanda0119/post/08ba8b85-2a4f-4e5c-b0f5-262452d9f0d3/image.png)

### MSS(Maximum Segment Size)란?
TCP 세그먼트에서 헤더를 제외한 순수 데이터(payload)의 최대 크기
UDP를 사용시 MSS 개념은 적용되지 않고, 단순히 MTU 기준으로 최대 페이로드 크기 계산이 됨
전송 계층 - MSS
네트워크 계층 - MTU
![](https://velog.velcdn.com/images/shypanda0119/post/ddb3b305-017c-4611-b559-aba149df04d8/image.png)

### PMTUD(Path MTU Discovery)란?
송신자가 DF(Don't Fragment) 플래그가 설정된 패킷을 보내고, 경로상의 라우터가 패킷이 너무 크다고 판단하면 패킷을 폐기한 뒤 ICMP Fragmentation Needed 메시지를 반환. 송신자는 이 메시지를 바탕으로 패킷 크기를 점진적으로 줄여가며 전송을 반복하고, 더 이상 오류가 발생하지 않을 때까지 과정을 이어가 최종적으로 경로에서 허용되는 최대 패킷 크기(Path MTU)를 알아내는 과정

# 애플리케이션 계층(Application)
HTTP, SMTP, SSH, FTP가 대표적이며 웹 서비스, 이메일 등 서비스를 실질적으로 사람들에게 제공하는 층

#### HTTP(Hypertext Transfer Protocol)란?
처음에는 서버와 브라우저간에 데이터를 주고 받기 위해 설계된 프로토콜, 지금은 브라우저 뿐만 아니라 서버와 서버간의 통신할 때도 많이 이용

1. HTTP는 헤더를 통한 확장이 쉬움
2. HTTP는 stateless


#### SSH(Secure Shell Protocol)란?
보안되지 않은 네트워크에서 네트워크 서비스를 안전하게 운영하기 위한 암호화 네트워크 프로토콜

#### FTP(File Transfer Protocol)란?
노드와 노드간의 파일을 전송하는데 사용되는 프로토콜, 지금은 파일을 암호화해서 전송하는 FTPS 또는 SFTP로 대체

#### SMTP(Simple Mail Transfer Protocol)란?
인터넷을 통해 메일을 보낼 때 사용되는 프로토콜

# 전송 계층(Transport)
TCP, UDP가 대표적이며 애플리케이션 계층에서 받은 메시지를 기반으로 세그먼트 또는 데이터그램으로 데이터를 쪼개고 데이터가 오류없이 순서대로 전달되도록 도움을 주는 층

### TCP

#### 가상회선 패킷교환 방식
![](https://velog.velcdn.com/images/shypanda0119/post/123d2355-4252-4c31-80db-e6c059f0bb07/image.png)

#### 오류검사 메커니즘
1. 재전송 : 시간 초과 기간이 지나면 서버는 전달되지 않은 데이터에 대해 재전송을 시도
2. 체크섬 : 체크섬을 통해 무결성을 평가. 즉, 송신된 데이터의 체크섬과 수신된 데이터의 체크섬 값을 비교해서 올바르게 왔는지를 확인(헤더는 20 ~ 60 바이트로 가변적)

### TCP 연결성립 : 3-웨이 핸드셰이크
1. SYN 단계 : 클라이언트는 서버에 클라이언트의 ISN을 담아 SYN을 보냄
2. SYN + ACK 단계 : 서버는 클라이언트의 SYN을 수신하고 서버의 ISN을 보내며 승인번호로 클라이언트의 ISN + 1을 보냄
3. ACK 단계 : 클라이언트는 서버의 ISN + 1한 값인 승인번호를 담아 ACK를 서버에 보냄
![](https://velog.velcdn.com/images/shypanda0119/post/812d2c59-e84e-43a9-9a0d-4b1e2dd164d2/image.png)
![](https://velog.velcdn.com/images/shypanda0119/post/b55e3fde-eecd-4a07-8e89-f1a42fcc95a3/image.png)
**클라이언트와 서버의 상태**
TCP 연결을 하면서 클라이언트는 closed, syn-sent, established가 되어 server는 closed, listen, syn_received, established 상태가 됨

### TCP 연결해제 : 4-웨이 핸드셰이크
1. 클라이언트가 연결을 닫으려고 할 때 FIN으로 설정된 세그먼트를 보냄. 그리고 클라이언트는 FIN_WAIT_1 상태로 들어가고 서버의 응답을 기다림
2. 서버는 클라이언트로 ACK라는 승인 세그먼트를 보내고 CLOSE_WAIT 상테에 들어감, 클라이언트가 세그먼트를 받으면 FIN_WAIT_2 상태에 들어감
3. 서버는 LAST_ACK 상태가 되며 일정 시간 이후에 클라이언트에 FIN이라는 세그먼트를 보냄
4. 클라이언트는 TIME_WAIT 상태가 되고 다시 서버로 ACK를 보내서 서버는 CLOSED 상태가 되며, 이후 클라이언트는 어느 정도 시간(TIME_WAIT으로 설정된 시간)을 대기한 후 연결이 닫힘
![](https://velog.velcdn.com/images/shypanda0119/post/d9d20b30-4e61-458c-867f-72137c4c76b0/image.png)

#### TIME_WAIT
TIME_WAIT는 지연 패킷등이 발생했을 때 데이터 무결성을 해결하기 위해 패킷을 기다리는 시간(2 * MSL(Maximum Segment Lifetime)동안 기다림
또한, 연결이 올바르게 닫힌 상태로 만들기 위해서 존재




### UDP

#### 데이터그램 패킷교환 방식
![](https://velog.velcdn.com/images/shypanda0119/post/b1627550-546f-4922-b68b-db908e271942/image.png)

#### 오류검사 메커니즘
단순한 체크섬만 지원(헤더는 8바이트의 고정길이)

### TCP VS UDP 
![](https://velog.velcdn.com/images/shypanda0119/post/d3d2e469-dffa-4b4d-875c-910a10ab6179/image.png)

# 인터넷 계층(Network)
IP, ICMP, ARP가 대표적이며 한 노드에서 다른 노드로 전송 계층에서 세그먼트 또는 데이터그램을 패킷화하여 전송

#### ICMP(Internet Control Message Protocol)란?
노드와 노드 사이에서 통신이 잘되나를 확인(테스트)할 때 쓰는 프로토콜


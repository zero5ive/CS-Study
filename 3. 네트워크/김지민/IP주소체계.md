# IPv4와 IPv6
#### IPv4란?
32비트로 표현되는 주소체계이며 2^32개의 주소(41억 9천만)를 표현할 수 있음. 하지만, 이 주소체계만으로는 부족하기 때문에 NAT, 서브네팅 등 여러개의 부수적인 기술이 생겨남

#### IPv6란?
128비트로 표현되는 주소체계이며 2^128개의 주소를 표현
즉, 많은 주소 처리가능하며 IPv4에서 쓰였던 NAT, 서브네팅이 필요하지 않음
IPSec이 내장됐으며 단순해진 헤더 포맷을 가지고 체크섬을 가지고 있지 않음

# 클래스풀(Classful IP Addressing)
IP주소는 인터넷 주소로 네트워크 주소, 호스트 주소. 즉, 두 부분으로 나뉘며 네트워크 주소는 호스트들을 모은 네트워크를 지칭
- 네트워크 주소가 동일 = 로컬 네트워크
- 호스트주소 : 호스트를 구분하기 위한 주소
- 네트워크 호스트(network host)는 컴퓨터 네트워크에 연결된 컴퓨터나 기타 장치

### 정의
네트워크 주소를 매기고 그에 따라 네트워크의 크기를 다르게 구분하여 클래스를 할당하는 주소체계. 구분하는 구분자(1,2, 3옥텟)를 서브넷 마스크라고 함
![](https://velog.velcdn.com/images/shypanda0119/post/9676fd0d-8ec5-4a16-8dee-1b35493691c7/image.png)

#### 클래스 A
![](https://velog.velcdn.com/images/shypanda0119/post/8500f25a-3aba-4849-8e63-a632f33a99f5/image.png)

#### 클래스 B
![](https://velog.velcdn.com/images/shypanda0119/post/28a46dde-1754-44c2-bc51-679258cfc9e0/image.png)


#### 클래스 C
![](https://velog.velcdn.com/images/shypanda0119/post/93e265af-7d69-4b4b-8e32-bdaf5761f590/image.png)

# 클래스리스, 서브넷 마스크, 서브네팅
클래스풀의 단점을 해결하기 위해 클래스리스가 등장, 클래스로 나누는 것이 아닌 서브넷마스크를 중심으로 어디까지가 네트워크 주소고 어디까지가 호스트 주소인지를 나눔
- 서브네팅 : 네트워크를 나눈다는 의미
- 서브넷 : 서브 네트워크, 쪼개진 네트워크
- 서브넷마스크 : 서브네트워크를 위한 비트마스크

## 클래스풀 vs 클래스리스
#### 클래스풀 네트워킹(Classful Networking)
- IP 주소를 A,B,C,D,E 클래스 기반으로 구분
- 각 클래스는 고정된 서브넷 마스크(FSM)를 가지고 있음
	- 클래스 A: 255.0.0.0
    - 클래스 B: 255.255.0.0
    - 클래스 C: 255.255.255.0
- 고정된 서브넷 마스크를 사용하여 네트워크와 호스트 부분을 나눔
- IP 주소의 첫번째 옥텟에 따라 클래스가 결정됨

#### 클래스리스 네트워킹(Classless Inter-Domain Routing, CIDR)
- 클래스 기반의 제한을 없앰
- 고정된 서브넷 마스크 대신 가변 길이 서브넷 마스크(VLSM)를 사용하여 네트워크와 호스트 부분을 동적으로 나눔
- CIDR 표기법을 사용하여 네트워크를 나타냄
- 더 유연하게 네트워크를 할당하고, 주소낭비를 줄일 수 있음

# 공인IP(public IP)와 사설IP(private IP)와 NAT
IP주소의 부족을 공인IP(public IP)와 사설IP(private IP)로 나누고 중간에 NAT이라는 기술을 통해 해결

#### NAT(Network Address Translation)이란? 
패킷이 트래픽 라우팅 장치를 통해 전송되는 동안 패킷의 IP주소를 변경, IP 주소를 다른 IP 주소로 매핑하는 방법
![](https://velog.velcdn.com/images/shypanda0119/post/84e3afc7-4e96-4e37-932a-99f58ec8b451/image.png)

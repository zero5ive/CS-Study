# IP주소, MAC주소, ARP, RARP
#### IP 주소(Internet Protocol address)란?
논리적 주소이며 컴퓨터 네트워크에서 장치들이 서로를 인식하고 통신을 하기 위해서 사용하는 특수한 번호이며 IP를 기반으로 통신한다고 하지만 사실상 그 밑에 물리적 주소인 MAC 주소를 통해 통신

#### MAC 주소(Media Access Control Address)란?
네트워크 인터페이스에 할당된 고유식별자이며 보통 장치의 NIC에 할당
48비트로 이루어져있으며 24비트의 OUI와 24비트의 UAA로 이루어져 있음
- OUI : IEEE에서 할당한 제조사 코드
- UAA : 제조사에서 구별되는 코드

#### ARP와 RARP
![](https://velog.velcdn.com/images/shypanda0119/post/9aac7841-378e-4333-b02b-725896c8627e/image.png)
ARP를 통해 논리적 주소인 IP주소를 물리적 주소인 MAC 주소로 변환
RARP를 통해 물리적 주소인 MAC주소를 논리적 주소인 IP 주소로 변환

#### ARP 과정
![](https://velog.velcdn.com/images/shypanda0119/post/1bbc21cf-2e2c-42c2-b20b-07699638bc4f/image.png)
1. 해당 IP주소에 맞는 MAC주소를 찾기 위해 해당 데이터를 브로드캐스팅을 통해 연결된 네트워크에 있는 장치한테 모두 보냄
2. 맞는 장치가 있다면 해당 장치는 보낸 장치에게 유니캐스트로 데이터를 전달해 주소를 찾게 됨



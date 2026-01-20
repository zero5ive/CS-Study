# HTTPS와 TLS
### 암호화란?
누군가 내 데이터를 훔쳐보더라도 내용을 알 수 없게 하는 기술이며 어떠한 평문(plaintext)을 키 와 알고리즘을 기반으로 암호문(ciphertext)으로 바꾸는 기술. 또한, 만약 암호문이 탈취되더라도 키 없이는 복호화를 못하게 만드는 작업

#### 대칭 암호화(symmetric algorithm)란?
암호화(Encrypt)와 복호화(Decrypt)에 동일한 비밀키를 사용하는 방식

- AES(Advanced Encryption Standard)란?
스크램블을 사용한 대칭키 암호화 알고리즘으로 10라운드에 걸쳐 각 라운드 스크램블(SubBytes, ShiftRows, MixColumns), AddRoundKey(현재 상태에 키를 XOR 연산으로 더하는 단계) 등의 연산으로 데이터를 암호화하는 알고리즘

- 스크램블이란?
AES-128을 기준으로 스크램블을 설명하자면 128비트(=16바이트)의 데이터를 다음과 같은 4x4 바이트 매트릭스로 처리하고 다음과 같이 위치를 섞어 "패턴"을 복잡하게 만드는 것

#### 비대칭 암호화(Asymmetric Encryption)란?
서로 다른 두 개의 키(공개키, 개인키)를 사용하는 암호화 방식이며 대표적으로 RSA, DH(Differ-Hellman)가 있음
공개키로 암호화하면 -> 개인키로 복호화 가능
![](https://velog.velcdn.com/images/shypanda0119/post/bf89f8eb-3c64-4325-9a8e-24f8732eae9d/image.png)








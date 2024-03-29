# TCP/IP 4계층 모델

### 정의
- 인터넷 프로토콜 스위트(internet protocol suite)는 인터넷에서 컴퓨터들이 서로 정보를 주고받는 데에 쓰이는 프로토콜의 집합
- **TCP/IP 4계층** 혹은  **OSI 7계층** 모델이 많이 쓰인다
- 계층 모델이란, 네트워크에서 사용되는 통신 프로토콜의 집합
- TCP/IP 4계층 모델의 계층들은 프로토콜의 네트워킹 범위에 따라 네 개의 추상화 계층으로 구성된다

## 1.1 계층 구조

### TCP/IP 4계층
- 애플리케이션 계층 (FTP/HTTP/SSH/DNS 등)
- 전송 계층 (TCP/UDP 등)
- 인터넷 계층 (IP/ARP/ICMP 등)
- 링크 계층 (이더넷 등)

### 1. 애플리케이션 계층
- HTTP, FTP, SSH, DNS 등 응용 프로그램이 사용되는 프로토콜 계층
- 웹 서비스, 이메일 등 서비스를 실질적으로 제공하는 계층
> - FTP : 장치와 장치 간의 파일을 전송하는 데 사용되는 표준 통신 프로토콜
> - SSH : 보안되지 않은 네트워크에서 네트워크 서비스를 안전하게 운영하기 위한 암호화 네트워크 프로토콜
> - HTTP : World Wide Web을 위한 데이터 통신의 기초이자 웹 사이트를 이용하는 데 쓰는 프로토콜

### 2. 전송(transport) 계층
- 송신자와 수신자를 연결하는 통신 서비스를 제공
- 애플리케이션과 인터넷 계층 사이의 데이터가 전달될 때의 중계 역할
- 연결 지향 데이터 스트림 지원, 신뢰성, 흐름 제어 등 프로토콜마다 다양한 기능 제공
- TCP ,UDP 등이 이 계층에 속한다
- **TCP**(Transmission Control Protocol) : 
  - 가장 널리 쓰이는 전송 계층 프로토콜 (HTTP 2.0까지는 TCP를 사용)
  - 패킷 사이의 순서를 보장하고 연결을 통한 **신뢰성 구축**(3-way handshake)등 다양한 기능 제공
  - 패킷 교환 방식은 **가상 회선 방식**
- **UDP**(User Datagram Protocol)
  - 순서를 보장 하지 않고, 수신 여부를 확인하지 않는다
  - 패킷 교환 방식은 단순히 데이터만 주는 **데이터그램 패킷 교환 방식** 사용

### TCP vs UDP
- TCP 
  - TCP는 전송 순서 보장, 수신 여부 확인, 논리적 연결 수립/해제, 데이터의 흐름 제어나 혼잡 제어 등 **안정성**과 **신뢰성을 강점**으로 가진다
    - 위의 이유들 때문에 UDP 보다 속도가 느리다
    - **연속성보다 신뢰성**있는 전송이 중요할 때에 사용하는 프로토콜
      - ex) 파일 전송. 하지만 최근에는 동영상 스트리밍등에도 사용 된다 -> [넷플릭스](https://victoria-k.tistory.com/entry/%EC%99%9C-%EB%84%B7%ED%94%8C%EB%A6%AD%EC%8A%A4%EB%8A%94-%EB%B9%84%EB%94%94%EC%98%A4-%EC%8A%A4%ED%8A%B8%EB%A6%AC%EB%B0%8D%EC%97%90-UDP-%EB%8C%80%EC%8B%A0-TCP%EB%A5%BC-%EC%93%B0%EB%8A%94%EA%B0%80) 
- UDP
  - UDP는 TCP보다 **빠른 속도**를 가진다
    - UDP는 비연결형 서비스이기 때문에, 연결을 설정하고 해제하는 과정이 존재하지 않는다
    - 결국 3way handshake 같은 논리적 연결 과정(흐름 제어 또는 혼잡 제어)이 별도로 없다
    - **신뢰성보다는 연속성**이 중요한 서비스에 사용
      - ex) 실시간 서비스 (streaming)

> #### 가상회선 패킷 교환 방식
> - 각 패킷에는 가상회선 식별자가 포함된다
> - 모드 패킷을 전송하면 가상회선이 해제되고 패킷들은 **전송된 순서대로** 도착하는 방식
> #### 데이터그램 패킷 교환 방식
> - 패킷이 독립적으로 이동하며 최적의 경로로 간다
> - 하나의 메세지에서 분할된 여러 패킷은 서로 다른 경로로 전송될 수 있다
> - 도착한 **순서가 다를 수 있다**

### 3way handshake
- TCP에서 서버와 클라이언트 사이에 서로 **연결을 논리적으로 수립**하는 과정
- 아래 과정을 통해서 진행된다
  1. SYN 단계: 
    - 클라이언트는 ISN(고유 시퀀스)을 담아 -> 서버로 SYN(연결 요청 플래그) 전송
  2. SYN+ACK 단계:
    - 서버는 SYN 수신 -> 서버의 ISN을 클라이언트로 보냄 (승인번호 : 클라이언트 ISN + 1)
  3. ACK 단계:
    - 클라이언트는 승인번호를 담아 -> ACK(응답 플래그)를 서버로 전송
- **딱 봐도 신뢰성이 있어 보인다** 

### 4way handshake
- TCP에서 서버와 클라이언트 사이에 서로 **연결을 논리적으로 해제**하는 과정
- 아래 과정을 통해서 진행된다
  - 클라이언트가 연결을 닫으려 할때 -> 서버로 FIN 전송
  - 서버는 FIN 수신에 대한 응답으로 ACK 전송 -> 클라이언트가 받으면 일정 시간 대기 (`TIME_WAIT`)
  - 일정 시간 이후, 서버 -> 클라이언트로 FIN 전송
  - 클라이언트는 FIN 수신에 대한 응답으로 ACK 전송 -> 서버 닫힘 -> 어느 정도 대기 후 클라이언트도 닫힘
- `TIME_WAIT`은 왜 존재하는가?
  - 지연 패킷이 발생할 수 있다, 지연 패킷을 처리하지 못한다면 **데이터 무결성** 문제 발생 -> 해당 패킷이 도착하도록 잠시 기다린다
  - 두 장치가 연결이 닫혔는지 확인한다

### 3. 인터넷 계층
- 장치로부터 받은 패킷을 지정된 목적지로 전송하기 위해 사용되는 계층
- IP 등이 존재하며, 패킷을 수신해야 하는 상대의 주소를 지정하여 (예: IP 주소) 데이터를 전달한다
- 상대방이 제대로 받았는지에 보장하지 않는 비연결형적인 특징이 있다

### 4. 링크 계층
- 실질적으로 데이터를 전달하며 장치 간에 신호를 주고 받는 '규칙'을 정하는 계층
- 네트워크 접근 계층이라고도 한다
- `물리 계층`과 `데이터 링크 계층`으로 나뉜다
  - 물리 계층 : 무선 LAN과 유선 LAN을 통해 0,1로 이루어진 데이터를 보내는 계층
  - 데이터 링크 계층 : 이더넷 프레임을 통해 여러 에러 확인 및 흐름,접근 제어를 담당하는 계층

#### 유선 LAN
- 유선 LAN을 이루는 이더넷은 IEEE802.3이라는 프로토콜을 따른다 
- 이는 여러 제조업자들이 만들어내는 장치들 간에 상호 통신이 가능하게 하는 표준을 제정하기 위함이였으며, 주요 LAN 프로토콜인 물리층과 데이터링크 층의 기능들을 규정하였고 `전이중화` 통신을 쓴다
#### 전이중화 통신
- 전이중화(full duplex) 통신은 **양쪽 장치가 동시에 송수신** 할 수 있는 방식을 말한다
- 현대의 고속 이더넷은 이 방식을 기반으로 통신한다
#### 무선 LAN
- 무선 LAN 장치들은 송신과 수신에 같은 채널을 공유하기 때문에 `반이중화` 통신을 사용한다
#### 반이중화 통신
- 반이중화(half duplex) 통신은 **송수신을 동시에 통신할 수 없으며, 한 번에 한 방향만 통신**할 수 있는 방식을 말한다

### 계층 간 데이터 송수신 과정
- 데이터 전송 시
  - 애플리케이션 -> 전송 -> 인터넷 -> 링크
  - 전송시엔 `캡슐화`의 과정을 거친다
- 데이터 수신 시
  - 링크 -> 인터넷 -> 전송 -> 애플리케이션
  - 수신시엔 `비캡슐화`의 과정을 거친다
> #### 캡슐화
> - 상위 계층의 헤더와 데이터를, 하위 계층의 데이터 부분에 포함 시키고 해당 계층의 헤더를 삽입 하는 과정
> #### 비캡슐화
> - 하위 계층에서 상위 계층으로 가며 각 계층의 헤더 부분을 제거하는 과정<br/>
<br/>`객체지향의 캡슐화와 동일하지는 않지만 유사한 정의를 가진다`
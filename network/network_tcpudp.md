## TCP/IP 전송계층
TCP/IP 는 인터넷에서 사용하는 프로토콜 그룹을 말합니다.

종류 : Application layer(응용계층), Transport layer(전송계층), Internet layer, Network Access later 4계층이 있습니다.

그중에서 전송계층은 두 응용 계층사이에서의 **process-to-process** 통신을 제공합니다.

전송계층은 응용계층으로부터 메세지를 받아 전송계층 패킷으로 **캡슐화**하여 전송합니다.

전송계층의 주요 프로토콜은 TCP,UDP

TCP : **연결형, 신뢰성 전송** 프로토콜입니다. TCP 로 전송하는 패킷을 segment 라고 합니다.

UDP : **비연결형, 비신뢰성 전송** 프로토콜입니다. UDP 로 전송하는 패킷을 datagram 이라고 합니다.

* process : 응용계층에서 구동중인 프로그램, 각각의 process 는 자신의 port 번호를 갖습니다.
* 두 종단 사이의 통신은 패킷이라고 불리는 데이터 블록에 의해 이루어집니다.

## TCP (Transfer Control Protocol)
연결형, 신뢰성 전송 프로토콜입니다.

1) 연결지향적 서비스를 제공하기 위해 데이터를 전송하기 전, 먼저 두 호스트의 전송 계층 사이에 논리적 연결을 설립합니다. (connection setup) → 3way- handshaking

2) 데이터를 전송합니다.(data transfer)

3) 전송이 완료됐으면 연결을 해제합니다. (conntection termination) → 4way- handshaking

신뢰성있는 서비스를 제공하기 위해 TCP가 전체 스트림을 순서에 맞고 오류없이, 부분적인 손실이나 중복없이 전송하는 것을 보장합니다.

이를 가능하게 하는 것이 오류제어,흐름제어, 혼잡제어등이 있습니다.

* 오류제어 : 훼손된 segment의 감지 및 재전송, 손실된 segment의 재전송, 순서가 맞지 않게 도착한 segment 를 정렬하고 중복 segment 를 감지 및 폐기를 합니다.

* 흐름제어 : 데이터를 보내는 속도와 데이터를 받는 속도의 균형을 맞추는 것을 의미합니다.

ex) 큰 파일은 다운로드할때 다운로드된 파일의 일부분이 손상되거나 훼손되면 안되기 때문에 신뢰성이 보장되는 프로토콜을 사용돼야 합니다.
##  UDP (User Datagram Protocol)
비연결형, 비신뢰성 전송 프로토콜입니다.

논리적 연결을 설립하지 않고 바로 datagram 을 전송하는 비연결형 프로토콜입니다. 또한 오류제어,흐름제어,혼잡제어등을 제공하지 않는 간단한 프로토콜입니다.

이러한 단순성은 **적은 양의 오버헤드**를 갖기 때문에 작은 메세지를 보내거나 신뢰성을 크게 고려하지 않아도 되는 상황에서 사용합니다.

ex) live 방송과 같이 실시간 상호작용을 하는 응용프로그램을 사용한다고 할때 음성과 영상은 한프레임씩 전송을 하는데 만약 훼손되거나 손실된 프레임을 재전송 해야한다면 전체적으로 지연이 될 것입니다.

따라서 이러한 경우엔 UDP 를 통해 약간의 훼손된 패킷은 그냥 무시하고 나머지 패킷을 응용프로그램으로 전달합니다.


## TCP vs UDP
TCP 는 연결형, 신뢰성 프로토콜입니다. 연결지향적 서비스를 제공하기 위해 데이터를 전송하기 전, 3way handshaking 을 하여 전송계층끼리 논리적 연결을 합니다.

신뢰성있는 서비스를 제공하기 위해 오류제어,흐름제어,혼잡제어등을 실행합니다.

신뢰성을 보장하기 위해서 **header가 더 크고 속도가 비교적 느리다는 단점이 있습니다.**

UDP는 비연결형, 비신뢰성 프로토콜입니다. 데이터를 전송하기전의 연결이나 오류제어,흐름제어 등의 실행이 없습니다.

따라서 적은 양의 오버헤드를 가지고 수신여부를 확인하지 않기 때문에 속도가 빠릅니다.

→ TCP 는 신뢰성이 중요한 통신(Http,File전송 등)에 쓰이고, UDP 는 실시간성이 중요한 통신(동영상 스트리밍 등)에 주로 사용됩니다.


## 3-way handshake
3-way handshake 는 TCP/IP 프로토콜로 통신하기 전, 정확한 정보 전송을 위해 상대방 컴퓨터와 세션을 수립하는(연결하는) 과정입니니다. (**TCP연결 초기화**)

1) Client는 Server에 접속을 요청하는 SYN 패킷을 보냅니다.

2) Server는 Client에 요청을 수락하는 ACK를 포함하여 SYN + ACK 패킷을 보냅니다.

3) Client는 이를 수신한 후, 다시  Server에 ACK 패킷을 보냅니다.

이로써 데이터를 주고받을 수 있습니다.

## 4-way handshake
TCP connection termination은 양방향으로 2개의 연결이 독립적으로 닫히기 때문에 4-way handshake 의 단계를 밟게 됩니다.

1) Client process 에서 active close를 하면, client tcp 에서 FIN 세그먼트를 보냅니다.

2) Server는 FIN 세그먼트를 받았다는 ACK를 Client에게 보냅니다. 이때 Server 내의 process 에게 EOF를 보내지만, 아직 process 는 close되지 않을 수 있습니다.

3) Server process 에서 passive close 를 하면, Server tcp 에서 FIN 세그먼트를 Client tcp 에게 보냅니다.

4) Client 가 Server 에 ACK를 보냅니다.

## 예상 질문

1. TCP와 UCP에 대해 설명해주세요.
2. 3-way handshake의 동작과정에 대해 설명해주세요.

## 참고 자료

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->
- [인프런강의](https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%A0%84%EA%B3%B5%EB%A9%B4%EC%A0%91-cs-%EC%99%84%EC%A0%84%EC%A0%95%EB%B3%B5/dashboard)

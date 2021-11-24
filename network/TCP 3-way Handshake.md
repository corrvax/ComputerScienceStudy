<div align="center">
  <br />
  <h1> TCP 3-way Handshake</h1>
  <br />
</div>

## 목차

1. [**TCP 3-way Handshake 정의와 역할**](#1)
2. [**TCP 3-way Handshake 과정**](#2)
3. [**TCP 4-way Handshake 과정**](#3)

<br />

<div id="1"></div>

## TCP 3-way Handshake 의 정의와 역할

**정의**
TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 **정확한 전송을 보장하기 위해** 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 의미한다. 
<br/>
**역할**
1. 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 전달이 시작되기 전에 한쪽이 다른 쪽이 준비되었다는 것을 알수 있도록 한다. 
2. 양쪽 모두 상대편에 대한 초기 순차 일련번호를 얻을 수 있도록 한다.
<br />

<div id="2"></div>

## TCP 3-way Handshake 과정


![enter image description here](https://t1.daumcdn.net/cfile/tistory/99FB2A3D5B32ED7B0B)

(SYN 은 synchronize sequence numbers ACK는 acknowledgements 의 약자)

1. 클라이언트(A)는 서버(B)에 접속을 요청하는 SYN 패킷을 보낸다. 이때 클라이언트(A)는 SYN을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태가 된다.
2. 이때 서버(B)는 Listen 상태로 포트 서비스가 가능한 상태여야 한다. (Closed :닫힌상태) 서버(B)는 SYN 요청을 받고 클라이언트(A)에게 요청을 수락한다는 ACK와 SYN flag가 설정된 패킷을 발송하고 클라이언트(A)가 다시 ACK으로 응답하기를 기다린다. 이때 서버(B)는 SYN_RECEIVED 상태가 된다.
3. 클라이언트(A)는 서버(B)에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 된다. 이때의 서버(B) 상태가 성립(ESTABLISHED) 이다.

위와 같은 방식으로 통신하는것이 신뢰성 있는 연결을 맺어 준다는 TCP의 3 Way handshake 방식이다.

 
| 상태 | 설명 |
|--|--|
| Closed  | 닫힌 상태  |
| Listen  | 포트가 열린 상태로 연결 요청 대기중인 상태  |
| SYN-send| SYN 요청을 한 상태  |
| SYN-Received  | SYN 요청을 받고 상대방의 응답을 기다리는 상태  |
| ESTABLISHED | 연결이 확인된 상태  |


<br />

<div id="3"></div>

## TCP 4-way Handshaking 과정
**정의** 
세션을 종료하기 위해 수행되는 과정 

![enter image description here](https://t1.daumcdn.net/cfile/tistory/2152353F52F1C02835)

1. 클라이언트가 연결을 종료하겠다는 FIN플래그를 전송한다.
2. 서버는 클라이언트의 요청(FIN)을 받고 확인메시지(ACK)를 보내고 자신의 통신이 끝날때까지 기다리는데 이 상태가 **TIME_WAIT**상태다.  
3. 데이터를 모두 보내고 통신이 끝났으면 서버는 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다 .
4. 클라이언트는 FIN 메세지를 확인했다는 메세지(ACK)를 보낸다.
5. 클라이언트의 ACK 메세지를 받ㄷ은 서버는 소켓 연결을 Close 한다. 

**TIME_WAIT 이란?**
<br />
서버가 FIN을 전송하기 전에 전송한 ACK 패킷이 Routing 지연이나 패킷 유실로 인한 재전송으로 FIN 패킷보다 늦게 도착 할 수 있다. 이 경우 **데이터가 유실**되기 때문에 이를 **대비**하여 클라이언트는 서버로부터 FIN을 수신하더라도 **일정시간 (디폴트 240초) 동안 세션을 남겨 놓고 잉여 패킷을 기다리는 과정**을 말한다.  
  
  


<div align="center">
  <br />
  <h1>DNS Round Robin</h1>
  <br />
</div>

## 목차

1. [**DNS**](#1)
2. [**DNS Round robin**](#2)
3. [**DNS Round robin 단점해소 방법**](#3)

<br />

<div id="1"></div>

## DNS 

**DNS란?**
<br/>

Domain Name System 의 약자로서 IP 네트워크에서 사용하는 시스템이다.
즉, www.xxxx.com 과 같이 사람이 읽을 수 있는 이름을 192.0.0.1과 같은 숫자 IP주소로 변환하여 컴퓨터가 서로 통신 할 수 있도록 도와주는 서버이다.
-  DNS 시스템은 이름을 숫자로 매핑하여 마치 전화번호부와 같은 기능을 한다. 
 - DNS 서버는 이름에 대한 요청을 IP주소로 변환하여 최종 사용자가 도메인 이름을 웹 브라우저에 입력할 때 해당 사용자를 어떤 서버에 연결할 것인지는 제어한다. 이 요청을 쿼리 라고 한다.

<br />

**Domain 구조**

<br />

![enter image description here](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/lPmaS/btq4X6Ig1BQ/TuKGUCcyRyuzHkSxwaXg00/img.png)


<br />

1. 도메인은 전 세계적으로 고유하게 존재하는 이름이다. 즉, 정해진 규칙을 따라야하며 임의로 변경, 생성할 수 없다.
2.  모든 도메인은 "."(닷) 또는 루트라 불리는 도메인 아래에 역트리 구조로 계층적으로 구성되어 있다.
3. 루트 아래 단계를 최상위 도메인(TLD: Top Level Domain)이라고 부르며, 그 다음 단계는 도메인(SLD : Second Level Domain) 이라고 한다. 
4. 일반 최상위 도메인과 국가 최상위도메인으로 구분하며 일반 최상위 도메인은 스폰서 도메인과 언스폰서 도메인으로 구분된다.

<br />

**DNS 동작원리**

<br/>


 ![enter image description here](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bC6rMc/btq4VMRM01j/kfAfBy1ZHlrNUkb7ksiSS1/img.png)

<br />

 1. 주소를 브라우저에 입력 
 2.  Local DNS에게 IP 주소를 질의하여 캐시된 것에 없으면 다른 DNS 서버에 전달 (Root DNS)
 3.  ROOT 로 부터 com 도메인을 관리하는 TLD이름 서버 정보 전달 받는다.
 4. TLD에 "www.nvaer.com"질의 한다.
 5.  TLD에서 naver.com DNS 정보를 전달 받는다.
 6. "naver.com" 도메인을 관리하는 DNS 서버에 "www.naver.com" 호스트네임에 대한 IP 주소 질의
 7. Local DNS 서버에게 " www.naver.com에 대한 IP 주소는 222.122.195.6 응답
 8. Local DNS는 www.nvaer.com에 대한 IP 주소를 캐싱을 하고 IP 주소 정보를 전달한다.

<br/>

> 💡**Root DNS란?** <br/>
> 
> 인터넷의 도메인 네임 시스템의 루트 존이다. 루트 존의 레코드의 요청에 직접 응답하고 적절한 최상위 도메인에 대해 권한이 있는 네임 서버 목록을 반환함으로써 다른 요청에 응답한다.전세계에 961개의 루트 DNS가 운영되고 있다.

<br/>
※ ROOT -> COM -> xxx.com 서버를 차례대로 질의해서 답을 찾는 과정을 Recursive Query라고 한다.

<div id="2"></div>

## DNS Round robin

<br />

**DNS Round robin 란?**
<br/>
별도의 sw, hw 로드밸런싱 장비 없이 **오직 DNS 만을 이용해** 도메인 레코드 정보를 조회하는 시점에서 트래픽을 분산하는 기법으로 
웹 뿐만 아니라, 도메인을 사용하는 모든 서비스 (FTP, SMPT 등) 에 사용이 가능하다. 

<br />

**DNS Round robin 원리**

<br />

![enter image description here](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/yY2sc/btq4VBpjmAM/kSvBRPxrUUwGKVObTd08k1/img.png)

<br/>

1. 웹 서비스를 담당할 여러 대의 웹 서버는 자신의 공인 IP를 각각 가지고 있다.
2. 사이트 접속을 위해 사용자가 해당 도메인 주소를 브라우저에 입력하면 DNS는 도메인의 정보를 조회하는데 이때 IP주소를 여러 대의 서버 IP리스트 중에서 라운드 로빈 형태로 랜덤하게 하나 혹은 여러개를 선택하여 사용자에게 알려준다.
3. 결과적으로 웹 사이트에 접속하는 다수의 사용자는 실제로는 복수의 웹 서버에 나뉘어 접속하도 되면서 자연스럽게 서버의 부하가 분산되는 방식이다.
<br/>


**DNS Round robin 단점**
<br/>

1. 지리적으로 복수의 웹 서버가 멀리 떨어져 있어 **실시간 헬스 체크가 어렵다**.
	-   웹 서버의 부하가 높아 응답이 느려지거나, 접속 수가 꽉차는 등 서버가 문제가 생겨 서비스가 불가한 상태라도 DNS는 이를 인지 못하고 도메인 조회 결과에 포함시킨다.
	-    DNS 라운드 로빈은 어디까지나 부하분산 을 위한 방법이지 다중화 방법은 아니므로 다른 S/W 와 조합해서 관리할 필요가 있다.
	- HA(High Availability) 용도로는 적합하지 않다.
2. 서버의 수 만큼 공인 IP 주소가 필요함 부하 분산을 위해 **서버의 대수를 늘리기 위해서는 그 만큼의 공인 IP 가 필요하다**.
3. **DNS 조회 정보의 캐싱** 
	- 균등하게 분산되지 않아 모바일 사이트 등에서 문제가 될 수 있다.
		- 스마트폰의 접속은 캐리어 게이트웨이 라고 하는 프록시 서버를 경유 한다. 프록시 서버에서는 이름변환 결과가 일정 시간 동안 캐싱되므로 같은 프록시 서버를 경유 하는 접속은 항상 같은 서버로 접속된다. 
	-  PC 용 웹 브라우저도 DNS 질의 결과를 캐싱하기 때문에 균등하게 부하분산 되지 않는다. 
	- DNS 레코드의 Time To Live(TTL)값을 짧게 설정함으로써 어느 정도 해소가 되지만 TTL에 따라 캐시를 해제하는 것은 아니므로 반드시 주의가 필요하다.

> 라운드 로빈 DNS는 가용성을 제공하지 않기 때문에, 무중단 서비스가 필요한 시스템에는 어울리지 않는다. 단순히 여러 대의 웹 서버로 트래픽을 부하 분산할 때 가장 편리하게 사용할 수 있는 옵션이다. 
> 가용성이 필요한 시스템의 경우, Health Check기능이 포함된 DNS 서비스를 사용하는 것이 좋다. AWS Route53, Dyn DNS 서비스가 좋은 예다.

<br/>

<div id="3"></div>

## DNS Round robin 단점해소 방법

<br />

**Weighted round robin (WRR)**
<br/>
각각의 웹 서버에 가중치를 가미해서 분산 비율을 변경한다. 물론 가중치가 큰 서버일수록 빈번하게 선택되므로 처리능력이 높은 서버는 가중치를 높게 설정하는 것이 좋다.
<br/>

 **Least connection**
 <br/>
 접속 클라이언트 수가 가장 적은 서버를 선택한다. 로드밸런서에서 실시간으로 connection 수를 관리하거나 각 서버에서 주기적으로 알려주는 것이 필요하다.

## Network study 2022

- #### youtube채널 널널한개발자님의 네트워크 기초 강의를 정리해놓은 것 입니다.

---

<br/>

### L2 스위치
---

<img width="459" alt="스크린샷 2022-11-22 오후 8 39 29" src="https://user-images.githubusercontent.com/51349774/203305102-313605fa-b510-4935-aab6-011ee4ab88cc.png">

- L2(Data Link)계층에서 MAC(48bit)주소를 기반으로 스위칭한다.
- Endpoint와 직접 맞닿은 L2 스위치를 L2 ACCESS 스위치라 한다. 
- ACCESS 스위치들을 연결하는 스위치를 L2 DISTRIBUTION 스위치라 한다.
- L2 Access -> L2 DISTRIBUTION -> ROUTER 와 같이 더 큰 범위로 이어주는 역할을 하는 라인을 업링크라 부른다.

---
### IP와 IP HEADER 구조
---

> TCP/IP 패킷의 구조

<img width="412" alt="스크린샷 2022-11-22 오후 9 16 46" src="https://user-images.githubusercontent.com/51349774/203311689-ce2dc7d6-573d-4960-b408-176685b194dd.png">

> IP 패킷 구조

<img width="412" alt="스크린샷 2022-11-22 오후 9 16 46" src="https://upload.wikimedia.org/wikipedia/commons/f/f9/IPv4_header_%281%29.png">

<small>출처 : https://commons.wikimedia.org/wiki/File:IPv4_header_(1).png </small>

-  `version` : ip 프로토콜 버전을 나타낸다 .
-  `IHL(Internet Header Length)` : IP Header의 길이를 나타낸다 값은 주로 5이며 6일 경우 Option이 추가되었음을 의미한다.
-  `Identification ,Flags , Fragment offset`: 단편화에 관련된 정보들 (단편화:패킷이 MTU를 넘어설 경우  단편화가 일어나며  데이터가 나뉘는 것을 말한다.)
-  `TTL` : 패킷이 인터넷망의 라우터들을 거칠때마다 TTL 값은 1씩 감소한다 8비트 즉 0~255의 범위를 갖으며 TTL 값이 0이되면 라우터는 해당 패킷을 버린다.
-  `Protocol` : 4계층 헤더의 종류를 나타낸다. 이 값을 보고 TCP 혹은 UDP 헤더가 붙는지 알 수 있다. 
-  `Header checksum` : 전송간 오류가 있는지 체크하는 체크섬 값.
-  `Source address` : 출발지 IP 주소를 나타낸다.
-  `Destination address` : 목적지 IP 주소를 나타낸다.

> 패킷 단편화 
- 패킷이 인터넷 망에 존재하는 여러 라우터 거치는 중 MTU가 작은 라우터가 존재할 수 있다. ( 라우터 성능 발전으로 ,요즘엔 거의 없음)
- 이럴 경우 패킷의 단편화가 일어나는데 단편화가 일어난다는 것은 패킷의 개수가 늘어남을 의미하고 pps(packet per sec)가 증가된다.
- 인터넷의 속도를 측정하는 단위중 bps(bit per sec) 와 pps(packet per sec)가 있다 bps는 데이터의 총량을 나타내는 반면 pps는 전송되는 패킷의 갯수를 나타낸다 . 같은 용량의 데이터일때 pps 가 낮을 수록 통신속도가 빠름을 의미하며 pps를 낮추는게 중요하다.
- 단편화가 일어나지 않게 하기 위해 클라이언트와 서버는 낮은 MTU에 맞춰 자신들의 MTU를 하향 평준화하여 데이터를 전송한다.
- 단편화가 일어날 경우 보통 패킷의 재조립은 도착지 서버에서 한다 이떄 `Identification ,Flags , Fragment offset` 같은 값들이 사용된다.
- 현재 인터넷에선 라우터 성능 발전으로 단편화가 거의 일어나지 않지만 아예 일어나지 않는 것은 아니며 보통은 VPN 때문에 일어난다고한다. (조사필요)



---
### application proxy 구조와 작동
---


- 프록시는 우회 , 분석 ,보호 ,감시의 목적으로 사용된다.
- 클라이언트에서 프록시 설정을 해두면 클라이언트의 모든 트래픽은 프록시 서버를 거쳐서 목적지로 가게된다.
- 그 과정에서 우회 , 분석 ,보호 , 감시 등의 역할을 할 수 있다.
- 프록시는 클라이언트 뿐만 아니라 서버에게도 활용될 수 있으며 이러한 경우를 reverse proxy라 부른다.
- reverse proxy는 서버에 들어오는 트래픽을 먼저 받아 역할을 수행하고 실제 서버로 요청을 보낸후 서버의 응답을 클라이언트로 전달한다.
- 이때 보안의 목적으로 사용되는 reverse proxy를 WAF(Web Application Firewall)이라 부른다.



---
### TCP 프로토콜
---


<img width="412" alt="스크린샷 2022-11-22 오후 9 16 46" src="https://upload.wikimedia.org/wikipedia/commons/4/4e/TCP_Protocol_Diagram.png">
출처 :https://commons.wikimedia.org/wiki/File:TCP_Protocol_Diagram.png<br/>

-  ` Source port ` :  송신측 포트
-  ` Destination Port `:  수신측 포트를 의미한다.
-  `Sequence Number` : 32비트 2의 32승의 가용범위를 갖고 이를 용량으로 환산하면 4GB의 데이터를 표현할 수 있다.
-  `Acknowledgment Number` : 
-  `TCP Flags`:
-  `Window` : 수신측 윈도우 사이즈를 의미한다.
- 

<br/>

> 3-Way handshake

<img width="412" alt="스크린샷 2022-11-22 오후 9 16 46" src="https://s3.ap-south-1.amazonaws.com/afteracademy-server-uploads/what-is-a-tcp-3-way-handshake-process-three-way-handshaking-establishing-connection-6a724e77ba96e241.jpg">
출처 : https://afteracademy.com/blog/what-is-a-tcp-3-way-handshake-process 

<br/>

- tcp 에서 클라이언트와 서버를 연결하는 방식이다 . 
- 세그먼트 단위의 데이터를 클라이언트와 서버가 주고 받으며 서로의 sequence 번호 ,MSS(Maximum Segment Size),혼잡 제어 정책(네트웍에 문제가 있을 경우에 대한 정책 SACK(selective ack knowledgement)가 주로 사용된다.)을 교환한다.
- MSS가 다를 경우 MSS가 작은 쪽에 맞춰서 전송이 이뤄진다.
- 보안성을 갖고있지 않기 때문에 작정하면 속일 수 있다.

<br/>

> TCP/IP 통신과 L2 MAC 주소의 변화

- 클라이언트에서 데이터가 소캣->TCP/IP 을 지나  패킷이 생성되어 L2수준으로 내려올때 패킷은 FRAME화 되고
- FRAME 헤더에 출발지의 MAC 주소 , 목적지의 MAC주소가 바인딩 된다.
- 이떄 프레임이 생성된 출발지에서 첫 목적지는 L2 스위치(Access와 distribution)을 지나 게이트웨이(인터넷망과 닿아있는 라우터)의 MAC주소를 가리킨다. 
- 이제 프레임은 인터넷망을 구성하는 라우터를 지날때마다  출발지 , 목적지가 변경되면서 최종 끝단(Server)에 도달한다.
- 인터넷 망을 돌아다니는 과정 중 MAC주소는 계속 변경되나 패킷의 내용이 변경되지 않는다.

<br/>

> L2 스위치의 작동원리와 ARP(Address Resolution protocol)

<img width="601" alt="스크린샷 2022-11-25 오후 7 44 55" src="https://user-images.githubusercontent.com/51349774/203966410-6ff7b554-3198-480a-b366-dd026a59d972.png">

- ARP는 ip주소로 맥주소를 얻어내는 프로토콜을 말한다
- 위 그림에서 pc3번이 www.naver.com로 요청을 보낸다고 가정할때 자신이 게이트웨이로 설정한 192.168.0.1의 라우터의 맥주소를 얻어내야한다.(항상은 아님)
- 이때 ARP가 작동하는데 ARP의 과정은 아래와 같다.
- ARP를 속여 ARP spooping 공격이 가능하다.

1. pc3은 192.168.0.1인 호스트를 찾기위해  broadcast로 같은 네트워크대에 있는 모든 호스트에게 query를 날린다.
2. 192.168.0.1를 갖는 라우터는 자신의 MAC 주소(reply)를 pc3에게 unicast로 응답한다. 
3. pc3은 해당 값을 메모리에 저장한다 (ARP cache)


---
### TTL(TIME TO LIVE) 이란?
---

<img width="592" alt="스크린샷 2022-11-25 오후 10 34 47" src="https://user-images.githubusercontent.com/51349774/203996804-af109ee5-1bbd-4cb9-84a5-e0e4363eded1.png">


- 패킷이 목적지에 도착하기 전까지 라우터를 돌아다니는 수를 말하며 일정 횟수가 초과되면 해당 패킷이 버려진다.
- 2의 8승의 경우의 수를 갖으며 0~255  라우터 하나를 지날때마다 1씩감소하다 0이되면 패킷이 버려진다.
- 네트워크의 라우터가 꼭 계층적으로 이뤄져 있지는 않기 때문에 위와 그림과 같이 looping이 발생할 수 있는데
- looping이 지속될 경우 라우터가 뻗을 수 있다. 이를 막기 위해 TTL값이 사용된다.
- TTL 값이 0이되면 0이 되는 순간의 라우터는 ICMP (Internet control message protocol)로 해당 패킷 출발지 IP로 해당 패킷이 버려졌음을 알려준다. (보안 상의 문제로 항상 그렇진 않고 설정하기에 따라 다름)



---
### 서브넷, 서브넷 마스크
---
- 네트워크를 더 작은 단위로 분할해서 낭비를 막기위해 사용되는 방식이다.
- a b c 클래스의 아이피 주소 모두에서 사용될 수 있지만 c 클래스에서 가장 흔하게 사용된다.
- c 클래스 ip에서 네트워크 아이디 할당 비트는 24비트이다. 서브넷팅은 여기에 비트 하나를 더 부여함으써 마지막 비트로 2가지의네트워크를 구분하여 사용할 수 있게한다. 
- 나머지 7비트를 호스트아이디로 사용하기 때문에 c class 호스트 할당가능 수인 0 ~ 255 (8bit) 보다 더 작은 규모인 0 ~ 127 (7bit)로 사용하여 네트워크의 낭비를 막을 수 있다(ISP(internet service provider)입장에서)
- 유저입장에서도 브로드캐스트의 범위가 쓸데없이 늘어나기 때문에 네트워크 효율이 떨어질 수 있기 때문에 서브넷팅이 필요하다.
- 네트워크아이디를 25비트 이상으로도 부여할 수 있다. 늘린 비트수 만큼 2에 n승의 갯수로 네트워크가 나뉜다.
- c class ip에서 0(사용하지않음)과 255(broadcast id)를 할당할 수 없듯 서브넷팅된 네트워크 각각의 0번과 255번은 사용할 수 없다.
- 이는 더 작게 서브넷팅 될수록 사용할 수 있는 ip개수는 더 줄어드는 것을 의미한다. 때문에 너무 작은 단위로 서브넷팅하는 것 역시 낭비일 수 있다.


---
### 인터넷 공유기 작동원리 
---

<img width="595" alt="스크린샷 2022-12-06 오후 5 39 30" src="https://user-images.githubusercontent.com/51349774/205861951-a28ab8e8-ec57-402c-a609-4d18ebd395f8.png">


- 공유기는 L2 스위치와 라우터가 합쳐진 역할을 한다. 
- 공유기를 사용한다는 것은 IP 주소를 공유한다는 의미이다.  
- 인터넷공급업체로부터 할당 받은  Public IP는 공유기를 통해 NAT(network address translate)가 적용되어 여러개의 private ip에가 공유되어 사용된다.
- 위의 그림에서 PC가 네이버에 접속하려고 한다고 할때 PC의 요청패킷은 공유로 넘어가 한번 해석된다. 
- 공유기는 해당 패킷을 까서 로컬 IP , port ,  remote IP port 등을 NAT table에 저장한다 . 
- 다음으로 IP를 public ip로 port를 임의 포트로 변환한 후에 NAT table에 저장한 후 패킷을 외부망으로 보낸다.
- 패킷을 받는 네이버 입장에서는 공유기의 공인 IP만 보고 응답 패킷을 보내준다.
- 반대로 패킷이 들어올떄 (inbound) 공유기는 NAT table에 저장된 정보를 토대로 L2 스위칭하여 패킷을 endpoint로 전달한다.
- inbound 시에 NAT table과 일치하는 패킷만 필터링하여 자동으로 Firewall(방화벽)역할을 하기 때문에 공유기를 사용하면 보안성이 올라간다.



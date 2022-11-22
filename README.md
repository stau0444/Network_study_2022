## Network study 2022

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





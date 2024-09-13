# DNS

네트워크는 process간 통신이다. (단, 다른 호스트에서 실행되고 있는 process 간)

특정 process로 요청을 보내려면 그 process가 실행되고 있는 곳의 주소를 정확히 알아야 한다.  
 = IP 주소 : port 번호

host 이름에 해당하는 IP 주소를 어딘가에 기록해두고, 실제로 쓸 때는 host 이름만으로 그 process에 요청 보낼 수 있게 하자 = DNS

<br/>

## DNS: a distributed, hierarchical database

DNS 서버를 전세계에 단 한 대만 둔다면?

- 수많은 domain name - ip 주소 매핑을 단 한군데에서 관리하고 요청-응답해줘야 하므로 요청 대기 시간이 굉장히 길어짐
- DNS 서버 단 한 대가 문제 생기면 전세계 모든 사람이 domain name - ip 주소 매핑을 알 수 없게 됨.

= DNS 서버 단 하나로는 전서계의 ip주소록을 감당할 수 없음  
⇒ DNS 서버를 분산화, 계층화 시켜두었다.

![img](https://devjin-blog.com/static/df40acaf929fb371a270155e2ef49a36/72aae/browser_work_dns_2.png)

<br/>

## DNS: root name servers

최상위 도메인: .  
최상위에 있는 root name server는 전세계에 13군데 있다. (같은 copy를 갖고 있다)

<br/>

## TLD, authoritative servers

### top-level domain (TLD) servers

- com, org, net, edu 등의 도메인을 관리하는 서버

### authoritative DNS servers

- 네트워크를 운영하는 모든 기괸은 각자 자기자신의 authoritative DNS server를 운영해야한다.
- 각 기관마다, 자기 자신이 보유하고 있는 도메인에 속하는 host-ip 매핑은 자기가 책임지고 관리해야한다.

`naver.com`이라는 도메인 안에 속한 기기 중, host 이름을 가진 기기들이 있을 것임

- www 라는 이름이 붙은 기기
- api 라는 이름이 붙은 기기
- m 이라는 이름이 붙은 기기

이 host들의 이름 - 해당 기기의 IP 주소에 대한 매핑 정보를 authoritative DNS 서버가 갖고 있어야 한다.

### Local DNS name server

각 ISP 기관들이 host name - IP 주소 매핑 정보를 캐싱하고 있음

각 ISP 기관에 속한 사용자들은 가장 먼저 local DNS name server에 IP주소를 물어보고, 거기 cache에서 찾지 못하면 root name server로 나가서 찾는다.

### DNS IP 주소를 찾는 과정 예시

`cis.poly.edu` 라는 host가, `gaia.cs.umass.edu라는 host`로 요청을 보내려고 한다.

1. local DNS name server에 `gaia.cs.umass.edu` 호스트에 대한 IP 매핑 주소가 있는지 먼저 물어본다
2. 없으면, root DNS server로 가서 `gaia.cs.umass.edu` 호스트에 대한 IP 매핑 주소가 있는지 먼저 물어본다
3. root DNS server는 `gaia.cs.umass.edu`에 대한 IP 매핑 주소는 모르지만, edu 도메인을 관리하는 dns server(TLD DNS server)의 주소를 알고 있어서, 여기 DNS 서버로 가라고 알려준다.
4. TLD DNS server는 `gaia.cs.umass.edu`에 대한 IP 매핑 주소는 모르지만, `umass.edu` 도메인을 관리하는 authoritative DNS server의 주소는 알고 있어서, 여기 DNS 서버로 가라고 알려준다.
5. authoritative DNS server 에서는 `gaia.cs.umass.edu`에 대한 IP 매핑 주소를 알고 있어서, 매핑 정보를 응답으로 줄 수 있다.

<br/>

## DNS: caching, update records

Local DNS name server는 캐시 서버이다. 따라서, 원본과의 불일치 가능성이 있다

`naver.com` 도메인은 IP 주소가 1.1.1.1 이야 라고 캐싱하고 있었는데, 실제 `naver.com` 도메인의 IP 주소가 1.1.1.2로 바뀌면 캐시와 원본과의 불일치가 발생한다

- TTL (Time To Live): 이 캐시 데이터의 유효기간을 정한다. 특정 시간이 지나면, 원본 IP 주소를 다시 가져와 저장하도록 한다
  - TTL을 사용하더라도, 유효기간안에 원본 IP 주소가 바뀌면 host name으로 IP 주소 찾아올 수 없긴 하다. 그런데 애초에 IP 주소가 바뀌는 경우가 흔치 않고 웬만하면 TTL로 해결이 된다고 한다.. 그렇지만 그래도 IP 주소가 바뀌는 경우에 대비해 상위 DNS 서버에 notification을 보내는 무언가의 개념이 있다고 한다

<br/>

## DNS records

DNS IP 주소록에는 실제로 어떤 필드가 있는가

> **(name, value, type, ttl)**

### Type

- A
  - type=A이면, name 필드는 host name이고, value에 IP 주소가 들어있음을 의미한다
- CNAME
  - type=CNAME이면, name 필드는 별칭 host name이고, value에는 정식 host name이 들어있음을 의미한다.
- NS
  - type=NS이면, name 필드는 domain이고, value는 이 domain을 관리하는 host name이 들어있음 을 의미한다.
- MX
  - mail server와 관련된 이름

### Root Name server의 DNS 레코드 예시

| Name    | Value   | Type | TTL |
| ------- | ------- | ---- | --- |
| .edu    | dns.edu | NS   |     |
| dns.edu | 2.2.2.2 | A    |     |

- `edu` 도메인을 관리하는 name server의 host 이름은 `dns.edu` 이다.
- `dns.edu` host 이름에 대한 IP 주소는 2.2.2.2 이다.

항상 NS와 A 레코드는 한 쌍으로 같이 들어있다.

### 내가 만약 새로운 도메인으로 서버를 운영한다면?

`eunjin.com` 이라는 도메인으로 운영한다면, 일단 authoritative DNS 서버를 하나 운영해야 함.

authoritative DNS 서버의 host name: `dns.eunjin.com`, IP 주소: 1.1.1.1

`eunjin.com` 도메인의 DNS 레코드

| Name           | Value   | Type | TTL |
| -------------- | ------- | ---- | --- |
| www.eunjin.com | 1.1.1.2 | A    |     |
| api.eunjin.com | 1.1.1.3 | A    |     |
| dev.eunjin.com | 1.1.1.4 | A    |     |

이런식으로 DNS 레코드를 구성했다

그럼 이제 다른 사용자들이 내 authoritative DNS 서버를 찾을 수 있도록, 내 dns 서버의 IP 주소 정보를 어딘가에 저장해야 한다. `eunjin.com` 에서의 상위 도메인 = `com` 도메인의 DNS 서버에 저장해야한다.

`com` 도메인의 DNS 레코드

| Name           | Value          | Type | TTL |
| -------------- | -------------- | ---- | --- |
| .eunjin.com    | dns.eunjin.com | NS   |     |
| dns.eunjin.com | 1.1.1.1        | A    |     |

<br/>

## DNS: UDP protocol

DNS와 HTTP 모두 애플리케이션 계층에서 동작하는 프로토콜이다. 애플리케이션 하위 계층에서 제공하는 기능을 통해 네트워크 통신을 한다. 애플리케이션 하위 계층에서는 TCP/UDP 프로토콜 중 하나를 이용해 네트워크 통신을 한다.

HTTP는 TCP 프로토콜을 이용해 동작한다. 그런데 DNS는 UDP 프로토콜을 이용해 동작한다.

### 왜 DNS는 UDP 프로토콜을 이용하는가

UDP는 TCP보다 빠르다. (TCP 3-way handshake를 하지 않으니까) 대신 요청이 유실될 위험이 있다.

- DNS에서 주고받는 메시지 크기는 굉장히 작다. host name과 IP주소만 주고받으면 된다.
  - 메시지 크기가 작으므로 요청이 유실될 확률 자체가 작다
  - 메시지 크기가 작으므로 요청이 유실되더라도 손실이 작다. 다시 요청 보내면 되므로
- DNS는 결국에 HTTP 요청을 하기 위한 준비 동작이다. 그런데 이 준비 동작에서까지 handshake를 해가면서 요청을 주고받을 필요 없다.

⇒ 메시지가 유실되는 경우 발생하는 손해보다, UDP로 빠르게 메시지를 주고받는 것이 더 이득이기 때문에 UDP를 사용한다.

## 예상 질문

1. 브라우저에 `www.google.com`을 검색하면 어떤 일이 일어나나요?

## 참고 자료

<!-- 공부 과정에서 참고한 자료가 있다면, 첨부해주세요-->
<!-- * [자료주제](링크)  -->

- [생활코딩 - DNS의 원리](https://www.opentutorials.org/course/3276/20299)
- [KOCW - 컴퓨터 네트워크 (이석복)](http://www.kocw.net/home/cview.do?cid=6b984f376cfb8f70)
- [[번역] Browser에 www.google.com을 검색하면 어떤 일이 일어날까?](https://devjin-blog.com/what-happen-browser-search/)
- [브라우저에 URL을 입력했을 때 발생하는 일들](https://deveric.tistory.com/97)

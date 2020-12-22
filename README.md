HTTP 완벽 가이드
# 1장 HTTP 개관
HTTP (Hypertext Transfer Protocol)
## 1.1 HTTP: 인터넷의 멀티미디어 배달부
HTTP는 신뢰성 있는 데이터 전송 프로토콜을 사용하기 때문에, 먼 거리에도 데이터가 전송 중 손상되거나 꼬이지 않음을 보장한다.
## 1.2 웹 클라이언트 & 서버
웹 콘텐츠는 웹 서버에 보관한다. 클라이언트가 요청한 데이터를 제공한다.
HTTP 요청을 www.path.com 서버로 보낸다.
서버는 요청받은 객체 /index.html을 찾고, 성공했다면 여러 정보(해당 객체의 타입, 길이등)와 함께 HTTP 응답에 실어서 클라이언트에게 보낸다.
## 1.3 리소스
웹 리소스는 웹 콘텐츠의 원천이다.
간순한 리소스는 정적 파일이다. (.text, .html, .jpg 등등)
가능한 리소스에는 콘텐츠를 생성하는 프로그램도 포함된다. (라이브 영상, 검색등)
### 1.3.1 미디어타입
다양한 객체를 다루기 때문에, 각 객체에 MIME 타입이란 포맷 라벨을 붙인다.
Multipurpose Internet Mail Extensions는 서로 다른 이메일 서비스에서 메시지가 오갈때 발생하는 문제를 해결하기 위한 방법이였다.
HTTP에서도 멀티미디어 콘텐츠를 기술하고 라벨을 붙이는데 MIME를 활용한다.
MIME는 `/`로 구분된 문자열 라벨이다. `primary object type(주타입)/specific subtype(부타입)`
예시 : text/html, text/plain, image/jpeg, image/gif, video/quicktime, application/vnd.ms-powerpoint
### 1.3.2 URI
Uniform Resource Idenfier
URI를 통해 리소스를 고유하게 식벽하고 위치를 지정할 수 있다.
### 1.3.3 URL
Uniform Resource Locator
특정 서버의 한 리소스에 대한 구체적인 위치를 서술한다.
URL은 세 부분으로 이루어진 표준 포맷을 따른다.
- scheme : HTTP등 리소스에 접근하기 위해 사용되는 프로토콜을 서술한다.
- server : 서버의 인터넷 주소
- resource : 웹 서버의 리소스
### 1.3.4 URN
Uniform Resource Name
콘텐츠를 한 리소스에 대해 위치에 영향 받지 않는 유일무이한 이름 역할을 한다.
리소스의 위치가 변하거나, 다른 접속 프로토콜을 사용해도 문제 없다.
## 1.4 트랜잭션
HTTP 트랜잭션은 request와 response로 구성된다.
정형화된 데이터 덩어리인 HTTTP 메시지를 통해 이루어진다.
### 1.4.1 메서드
서버에게 어떤 동작을 취해야할지 알려주는 메서드
자주 사용하는 5개의 HTTP 메서드
- GET : 서버에서 클라이언트로 지정한 리소스를 보내라.
- PUT : 클라이언트에서 서버로 보낸 데이터를 지정한 이름의 리소스로 저장하라.
- DELETE : 지정한 리소스를 서버에서 삭제하라.
- POST : 클라이언트 데이터를 서버 게이트웨이 애플리케이션으로 보내라.
- HEAD : 지정한 리소스에 대한 응답에서 HTTP 헤더 부분만 보내라.
### 1.4.2 상태코드
모든 HTTP 응답 메시지는 상태 코드와 함께 반환
상태 코드는 요청이 성공했는지 아니면 추가 조치가 필요한지 알려주는 세 자리 숫자
각 숫자 상태코드에 text로 된 reason phrase도 함께 보낸다.
### 1.4.3 웹페이지는 여러 객체로 이루어질 수 있다.
애플리케이션은 하나의 작업을 수행하기 위해 여러 HTTP 트랜잭션을 수행한다.
## 1.5 메시지
HTTP 메시지는 단순한 줄 단위의 문자열이다.
이진 형식이 아닌 일반 텍스트형식으로 이루어진다.
클라이언트에서 서버로 보내는 request 메시지와 서버에서 클라이언트로 가는 response 메시지가 있다.
HTTP 메시지는 시작줄, 헤더, 본문으로 이루어진다.
- 시작줄 : 메시지의 첫줄, 어떤 요청인지(request) or 무슨일이 일어났는지(response) 적힌다.
- 헤더 : 0개 이상의 헤더 필드로 구성된다. 각 헤더 필드는 쉬운 구문분석을 위해 `:`으로 구분된 key & value로 구성된다. 헤더는 빈 줄로 끝난다.
- 본문 : 어떤 종류의 데이터든 들어갈 수 있는 메시지 본문, 이진 데이터나 텍스트도 포함 할 수 있다.
### 1.5.1 간단한 메시지의 예
```
GET / HTTP/1.1
Host: google.com
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 Whale/2.8.108.15 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
```
```
HTTP/1.1 301 Moved Permanently
Location: http://www.google.com/
Content-Type: text/html; charset=UTF-8
Date: Tue, 17 Nov 2020 07:59:12 GMT
Expires: Thu, 17 Dec 2020 07:59:12 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 219
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN
```
## 1.6 TCP 커넥션
메시지는 Tranmission Control Protocol 커넥션을 통해 한 곳에서 다른 곳으로 옮겨간다.
### 1.6.1 TCP/IP
HTTP는 애플리케이션 계층 프로토콜이다.
HTTP는 네트워크 통신의 핵심적은 세부사항에 대해서 신경 쓰지 않는다. 대신 대중적이고 신뢰성 있는 인터넷 전송 프로토콜인 TCP/IP에게 맡긴다.
TCP는 다음을 제공한다.
- 오류없는 데이터 전송
- 순서에 맞는 전달(데이터는 언제나 보낸 순서대로 전달된다.)
- 조각나지 않는 데이터 스트림(언제든 어떤 크기로든 보낼 수 있다.)
TCP/IP는 TCP와 IP가 층을 이루는 패킷 교환 네트워크 프로토콜 집합이다.
각 네트워크의 HW 특성을 숨기고, 어떤 종류의 컴퓨터와 네트워크든 서로 신뢰성 있는 의사소통을 가능하게 한다.
TCP 커넥션이 맺어지면 교환되는 메시지가 없어지거나, 손상되거나 순서가 뒤바뀌는 일은 일어나지 않는다.
HTTP 네트워크 프로토콜 스택
- HTTP : 애플리케이션계층
- TCP : 전송 계층
- IP : 네트워크 계층
- 네트워크를 위한 링크 인터페이스 : 데이터 링크 계층
- 물리적인 네트워크 하드웨어 : 물리 계층
### 1.6.2 접속, IP 주소 & port번호
Internet Protocol 주소와 port번호를 사용해 클라이언트와 서버 사이에 TCP/IP 커넥션을 맺는다.
URL을 통해 IP 주소와 port번호를 입력한다.
### 1.6.3 Telnet을 이용한 실제 예제
`telnet www.joes-hardware.com 80` : 해당 Host의 IP 주소를 찾아 80번 포트에 TCP 커넥션을 맺는다.
`GET /tools.html HTTP/1.1\nHost: www.joes-hardware.com` : 리소스 /tools.html을 요청한다.
## 1.7 Protocol 버전
HTTP/0.9
- 91년의 HTTP 프로토타입, 간단한 HTML 객체 받아오는것이 목적
- GET 메서드만 지원
- MIME & HTTP 헤더 및 버전 번호등 미지원
HTTP/1.0
- 처음으로 널리 쓰이기 시작한 HTTP 버전
- 버전번호, HTTP 헤더 및 추가 메서드 및 멀티미디어 객체 처리 지원
- 시작적으로 웹페이지와 상호작용하는 폼을 실현
HTTP/1.0+
- 90년대 중반 WWW 팽창에 따른 요구들을 만족시키기 기능 추가(비공식이지만 사실상 표준)
- keep-alive Connection, 가상 호스팅, 프락시 연결 지원
HTTP/1.1
- HTTP 설계의 구조적 결함 교정 & 성능 최적화 & 잘못된 기능 제거
- 더 복잡해진 웹 앱과 배포를 지원
HTTP/2.0
- 성능 문제를 개선하기 위해 구글의 SPDY 프로토콜 기반 설계 진행중인 프로토콜
## 1.8 웹의 구성요소
- Proxy: Client와 Server 사이의 HTTP 중개자
- Cash: Web Page를 Client 가까이 보관하는 HTTP 창고
- Gateway: 다른 앱과 연결된 특별한 Web Server
- Ternel: HTTP 통신을 전달하기만 하는 특별한 Proxy
- Agent: 자동화된 HTTP 요청을 만드는 웹 클라이언트
### 1.8.1 프락시
- 보안을 위해 사용
- 웹 트래픽 흐름 속에서 신뢰가능한 중개자 역할
- ex: 바이러스 검출, 미성년자 성인 콘텐츠 차단
### 1.8.2 캐시
- 웹 캐시와 캐시 프락시는 자주 찾는 것의 사본을 저장하는 HTTP Proxy Server
### 1.8.3 게이트웨이
- 다른 Server 들의 중개자
- HTTP 프로토콜을 다른 프로토콜로 변환하기 위해 사용
- 스스로가 리소르를 갖는 진짜 서버처럼 요청을 다룬다.
### 1.8.4 터널
- 두 커넥션 사이에서 raw data를 열어보지 않고 전달해주는 HTTP 어플리케이션
- 비HTTP 데이터를 HTTP 연결을 통해 그대로 전송하기 위해 사용된다.
- 예시=>HTTPS: 암호화된 SSL 트래픽을 HTTP 커넥션을 통해 전송
### 1.8.5 에이전트
- 사용자를 위해 HTTP 요청을 만들어주는 Client 프로그램
- 예시: 웹브라우저, 웹로봇(스파이더)
## 1.9 시작의 끝
- HTTP의 멀티미디어 전송 프로토콜의 역할에 주목하였다.
- URI로 원격 서버의 리소스에 이름을 어떻게 붙이는지 보았고,
- HTTP를 사용하는 몇몇 앱에 대해 조사하며 마무리했다.
- 앞으로, HTTP 프로토콜, 애플리케이션, 리스소 구조에 대해 상세히 살펴본다.
## 1.10 추가 정보
### 1.10.1 HTTP Protocol에 대한 정보
### 1.10.2 역사적 시작
### 1.10.3 기타 WWW 정보
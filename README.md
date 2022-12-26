# Http 웹 기본 지식

> [인프런. Http 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)

## 인터넷 통신

- IP(인터넷 프로토콜)
  - 지정한 IP 주소(IP Address)에 데이터 전달
  - 패킷(Packet)이라는 통신 단위로 데이터 전달

- IP 프로토콜의 한계
  - 비연결성
    - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
  - 비신뢰성
    - 중간에 패킷이 사라지면?
    - 패킷이 순서대로 안오면?
  - 프로그램 구분
    - 같은 IP 를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이라면?

## TCP, UDP

IP 프로토콜의 한계점을 해결하기 위한 것이 TCP, UDP 이다.

![img](/images/1.JPG)

- TCP 특징
  - 전송 제어 프로토콜(Transmission Control Protocol)
  - 연결지향 - TCP 3 way handshake (가상연결)
  - 데이터 전달 보증
  - 순서 보장
  - 신뢰할 수 있는 프로토콜
  - 현재는 대부분 TCP 사용

![img](/images/2.JPG)

![img](/images/3.JPG)

![img](/images/4.JPG)

위 그림 처럼 순서 보장이 가능한 이유는 TCP 정보에는 `전송 제어, 순서, 검증 정보` 등이 추가가 되어있다.

- UDP 특징
  - 사용자 데이터그램 프로토콜(User Datagram Protocol)
  - 하얀 도화지에 비유(기능이 거의 없음)
  - 연결지향 - TCP 3 way handshake X
  - 데이터 전달 보증 X
  - 순서 보장 X
  - 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
  - IP와 거의 같다. +PORT +체크섬 정도만 추가
  - 애플리케이션에서 추가 작업 필요
  
## Port

![img](/images/5.JPG)

- 0 ~ 65535 : 할당 가능
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
- FTP - 20, 21
- TELNET - 23
- HTTP - 80
- HTTPS - 443

## DNS

DNS(Domain Name System) 도메인 명을 IP 로 변환

![img](/images/6.JPG)

## URI 와 웹 브라우저 요청 흐름

- URI(Uniform Resource Identifier)
  - URN(Uniform Resource Name)
    - 리소스에 이름을 부여
    - 이름은 변하지 않는다.
    - URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
    - urn:isbn:8960777331 (어떤 책의 isbn URN)
  - URL(Uniform Resource Locator) 
    - 리소스가 있는 위치를 지정
    - 위치는 변할 수 있다.
  
- URI 단어 의미
  - Uniform : 리소스 식별하는 통일된 방식
  - Resource : 자원, URI 로 식별할 수 있는 모든 것
  - Identifier : 다른 항목과 구분하는데 필요한 정보
  
![img](/images/7.JPG)

### URL

- 문법
  - `scheme://[userinfo@]host[:port][/path][?query][#fragment]`
  - https://www.google.com:443/search?q=hello&hl=ko

- `scheme`
  - 주로 프로토콜 사용
  - 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
    - ex) http, https, ftp 등
  - http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
  - https는 http에 보안 추가 (HTTP Secure)
- `userinfo`
  - URL 에 사용자 정보를 포함해서 인증
  - 거의 사용 안함
- `host`
  - 호스트명
  - 도메인명 또는 IP 주소를 직접 사용 가능
    - ex) www.google.com
- `port`
  - 접속 포트
  - 일반적으로 생략(http는 80, https는 443)
- `path`
  - 리소스 경로, 계층적 구조
    - ex) /members/100, /items/iphone12
- `query`
  - key=value 형태
  - `?`로 시작 `&`로 추가 가능 
    - ?keyA=valueA&keyB=valueB
  - query parameter, query string 등으로 불린다. 
  - 웹 서버에 제공하는 파라미터
- `fragment`
  - html 내부 북마크 등에 사용
  - 서버에 전송하는 정보 아님

# HTTP(HyperText Transfer Protocol)

- `HTTP 메시지에 모든 것을 전송`
  - HTML, TEXT
  - IMAGE, 음성, 영상, 파일
  - JSON, XML
  - 거의 모든 형태의 데이터 전송 가능
  - 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
  
- `역사`
  - HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
  - HTTP/1.0 1996년: 메서드, 헤더 추가
  - `HTTP/1.1` 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전
  - RFC2068 (1997) -> RFC2616 (1999) -> RFC7230~7235 (2014)
  - HTTP/2 2015년: 성능 개선
  - HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선
  
- `사용 추세`
  - TCP: HTTP/1.1, HTTP/2
  - UDP: HTTP/3
  - 현재 HTTP/1.1 주로 사용
  - HTTP/2, HTTP/3 도 점점 증가

- `특징`
  - 클라이언트 서버 구조
    - Request Response 구조
    - 클라이언트는 서버에 요청을 보내고, 응답을 대기
    - 서버가 요청에 대한 결과를 만들어서 응답
    - `클라이언트 서버로 구조를 나누면 좋은점은 비지니스로직이나 데이터를 서버에 전부 밀어넣고, 클라이언트는 UI 와 UX 에 집중한다. 이렇게되면 클라이언트와 서버가 각각 독립적으로 진화할 수 있다. 즉, 클라이언트는 복잡한 비지니스 로직을 다룰 필요가 없게된다.`
  - 무상태 프로토콜(stateless)
    - 서버가 클라이언트의 상태를 보존X
    - 장점: 서버 확장성 높음(스케일 아웃)
    - 단점: 클라이언트가 추가 데이터 전송
    - 무상태는 응답 서버를 쉽게 바꿀 수 있다. -> 무한한 서버 증설 가능
  - 비연결성
    - 일반적으로 초 단위의 이하의 빠른 속도로 응답
    - 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
  - HTTP 메시지
  - 단순함, 확장 가능
 
- `실무 한계`
  - 모든 것을 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있다.
  - 무상태
    - 예) 로그인이 필요 없는 단순한 서비스 소개 화면
  - 상태 유지
    - 예) 로그인
    - 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
    - 일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지
    - 상태 유지는 최소한만 사용

- `비 연결성 한계와 극복`
  - TCP/IP 연결을 새로 맺어야 함 - 3 way handshake 시간 추가
  - 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등 수 많은 자원이 함께 다운로드
  - 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
  - HTTP/2, HTTP/3에서 더 많은 최적화
  
![img](/images/8.JPG)

![img](/images/9.JPG)

## 스테이스리스를 기억하자(서버 개발자들이 어려워하는 업무)

- 정말 같은 시간에 딱 맞추어 발생하는 대용량 트래픽
  - ex) 선착순 이벤트, 명절 KTX 예약, 학과 수업 등록
  - ex) 저녁 6:00 선착순 1000명 치킨 할인 이벤트 -> 수만명 동시 요청
  
대용량 트래픽은 최대한 머리를 쥐어짜서 stateless 하게 만들어야한다. stateless 는 스케일 아웃의 장점이 있으므로 대용량 트래픽이 발생하면
서버를 확 늘려서 대응을 할 수 있는 부분들이 많아진다.

그래서 이벤트 설계시 다음과 같은 방식으로 많이한다. 첫 페이지는 로그인도 필요없는 정적 페이지만 뿌린다.(상태없는 순수한 html) 그리고 사람들이
그 페이지에서 이것저것 보고 머무르는 시간을 가지게끔 한다음에 이벤트 참여 버튼을 누르게하거나 한다.

## HTTP 메시지

> [표준 스펙(RFC-7230)](https://tools.ietf.org/html/rfc7230#section-3)

![img](/images/10.JPG)

요청 메시지도 응답 메시지 처럼 body 를 가질 수 있다.

### 요청 메시지

> start-line = request-line / status-line
>
> request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)

#### 시작 라인

- HTTP 메서드 (GET: 조회)
  - GET : 리소스 조회
  - POST : 요청 내역 처리
- 요청 대상 (/search?q=hello&hl=ko)
  - `absolute-path[?query] (절대경로[?쿼리])`
  - 절대경로= "/" 로 시작하는 경로
  - http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다.
- HTTP Version
- HTTP 상태 코드 : 요청 성공과 실패를 나타냄
  - 200: 성공
  - 400: 클라이언트 요청 오류
  - 500: 서버 내부 오류
- 이유 문구 : 사람이 이해할 수 있는 짧은 상태 코드 설명 글

#### HTTP 헤더

```
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
```

> header-field = field-name ":" OWS field-value OWS (OWS:띄어쓰기 허용)
> 
> field-name은 대소문자 구문 없음

- 용도
  - HTTP 전송에 필요한 모든 부가정보
  - ex) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...
  - [표준 헤더](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
  
#### HTTP 메시지 바디

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte 로 표현할 수 있는 모든 데이터 전송 가능

## HTTP API URI 설계

- 회원 목록 조회 /read-member-list
- 회원 조회 /read-member-by-id
- 회원 등록 /create-member
- 회원 수정 /update-member
- 회원 삭제 /delete-member

이것은 좋은 URI 설계일까?

가장 중요한 것은 `리소스 식별`이다.

#### API URI 고민

- 리소스의 의미는 뭘까?
  -  회원을 등록하고 수정하고 조회하는게 리소스가 아니다!
  - 예) 미네랄을 캐라 -> 미네랄이 리소스
  - 회원이라는 개념 자체가 바로 리소스다.
-  리소스를 어떻게 식별하는게 좋을까?
  - 회원을 등록하고 수정하고 조회하는 것을 모두 배제
  - 회원이라는 리소스만 식별하면 된다. -> 회원 리소스를 URI 에 매핑
  
#### API URI 설계

- 회원 목록 조회 : /members - GET
- 회원 상세 : /members/{id} - GET
- 회원 등록 : /members - POST
- 회원 수정 : /members/{id} - PATCH, PUT, POST
- 회원 삭제 : /members/{id} - DELETE

> 참고: 계층 구조상 상위를 컬렉션으로 보고 복수단어 사용 권장(member -> members), 예를들어 주문(order) 이면 orders 이런식으로 리소스를 식별할 수 있도록 URI 를 만들어야 한다.

#### 리소스와 행위를 분리

가장 중요한 것은 `리소스를 식별`하는 것

- `URI 는 리소스만 식별`
- `리소스`와 해당 리소스를 대상으로 하는 `행위(메서드)`를 분리
  - ex) 미네랄(리소스)을 캐라(행위), 회원(리소스)을 등록(행위)하라
    - 리소스 : 미네랄, 회원
    - 행위(메서드) : 조회, 등록, 삭제, 변경

## HTTP 메서드

> [HTTP 메서드 더 자세한 내용 보기](https://github.com/BAEKJungHo/restful_basic/wiki/HTTP-Methods)

### GET: 리소스 조회
  
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- `메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 서버들이 많아서  권장하지 않음`

- 클라이언트가 서버의 리소스를 요청할 때 사용
- 캐시 사용 하는 경우 최종 결과가 캐시에 저장됨(캐싱 사용 가능)
- 브라우저 기록에 남음
- 북마크 가능
- 민감한 데이터 보낼 때 사용 금지(URL 에 노출됨)
- URL 데이터 길이 제한 약 2000 자 정도됨
- 안전한 메서드
- idemponent

### POST: 요청 데이터 처리, 주로 등록에 사용

> 스펙: POST 메서드는 대상 리소스가 리소스의 고유 한 의미 체계에 따라 요청에 포함 된 표현을 처리하도록 요청합니다. (구글 번역)

- 요청 데이터 처리
- `메시지 바디를 통해 서버로 요청 데이터 전달`
- 서버는 요청 데이터를 처리
- 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 `신규 리소스 등록, 프로세스 처리`에 사용

- 캐시가 가능하긴한데 본문 내용까지 캐시 키로 고려해야하는데 구현이 어렵다. 사실상 GET, HEAD 정도만 캐시로 사용한다.
- 브라우저 기록에 남지 않음
- 북마크 불가능
- 데이터 길이 제한 없음

- 예를 들어 POST는 다음과 같은 기능에 사용됩니다.
  - HTML 양식에 입력 된 필드와 같은 데이터 블록을 데이터 처리 프로세스에 제공
    - 예) HTML FORM 에 입력한 정보로 회원 가입, 주문 등에서 사용
  - 게시판, 뉴스 그룹, 메일링 리스트, 블로그 또는 유사한 기사 그룹에 메시지 게시
    - 예) 게시판 글쓰기, 댓글 달기
  - 서버가 아직 식별하지 않은 새 리소스 생성
    - 예) 신규 주문 생성
  - 기존 자원에 데이터 추가
    - 예) 한 문서 끝에 내용 추가하기
    
> 정리: 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함 -> 정해진 것이 없음

정리하자면 다음과 같다.

1. 새 리소스 생성(등록)
  - 서버가 아직 식별하지 않은 새 리소스 생성
2. 요청 데이터 처리
  - 단순히 데이터를 생성하거나, 변경하는 것을 넘어서 프로세스를 처리해야 하는 경우
    - 예) 주문에서 결제완료 -> 배달시작 -> 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우
  - POST 의 결과로 새로운 리소스가 생성되지 않을 수도 있음
    - 예) POST /orders/{orderId}/start-delivery (컨트롤 URI)
3. 다른 메서드로 처리하기 애매한 경우
  - 예) JSON으로 조회 데이터를 넘겨야 하는데, GET 메서드를 사용하기 어려운 경우
  - 애매하면 POST
  
> 사실 POST 는 전부 가능하다. 하지만 조회 같은 경우는 GET 을 쓰는게 유리한데, 서버끼리 약속이 되어있기 때문이다. GET 을 사용하면 캐싱이
쉽다는 장점 등이 있다. 반면 POST 는 캐싱이 어렵다.
  
### PUT: 리소스를 대체, 해당 리소스가 없으면 생성

- 리소스를 대체
  - 리소스가 있으면 대체
  - 리소스가 없으면 생성
  - 쉽게 이야기해서 덮어버림
- 중요! 클라이언트가 리소스를 식별
  - 클라이언트가 리소스 위치를 알고 URI 지정
  - POST 와 차이점
  
- 캐시가 가능하긴한데 본문 내용까지 캐시 키로 고려해야하는데 구현이 어렵다. 사실상 GET, HEAD 정도만 캐시로 사용한다.
- POST 와 다른점은 URI 에 대한 의미가 다르다
  - POST 의 URI 는 보내는 데이터를 처리할 리소스 지칭
  - PUT 의 URI 는 보내는 데이터에 해당하는 리소스 지칭
- idemponent

  
![img](/images/11.JPG)

![img](/images/12.JPG)

### PATCH: 리소스 부분 변경

- PUT 과 비슷하지만, 기존 에티티와 새 데이터의 차이점만 보낸다는 차이가 있다.
- idemponent

![img](/images/13.JPG)

![img](/images/14.JPG)

### DELETE: 리소스 삭제

- URI 에 해당하는 리소스를 삭제할 때 사용한다.
- 복수의 DELETE 요청은 단일 DELETE 요청과 동일하다.
- idemponent

### GET vs POST

POST 든 GET 이든 보내는 데이터는 전부 클라이언트측에서 볼 수 있다. 단지 GET방식은 URL에 데이터가 표시되여 별다른 노력없이 볼 수 있어서지, 두 방식 전부 보안을 생각한다면 암호화 해야한다.

GET 방식이 POST 방식보다 속도가 빠른것은 맞다. 그 이유는 GET 방식은 최종 결과가 캐시에 저장되기 때문에 같은 리소스 요청시 last-modified 헤더를 통해서 리소스 변경이 있는 경우는 서버에서 다시 접근하여 리소스를 요구하고, 변경된 리소스가 없으면 캐시된 리소스로 접근하기 때문에 빠른것이다.

POST 는 일반적으로 서버에서 리소스 변경을 해야하는 경우에 사용하는것으로 알고 있는데 POST 방식으로도 리소스를 GET 처럼 요청만 하기 위해서 사용할 수도 있다. GET 으로 보내야 하는 데이터가 많은 경우에 그렇다.

### PUT vs POST

POST 메서드는 요청을 처리할 엔티티를 Request-URI 로 지정하지만, PUT 메서드는 Request-URI 자체에 이미 엔티티가 포함되어있다.

ex) POST /v1/coffees/orders 는 주문 데이터를 생성한 뒤 생성된 리소스를 가리키는 식별자 URI 를 리턴한다. 반면 PUT /v1/coffees/orders/1234 는 주문번호 1234 의 리소스가 존재하면 업데이트하고, 존재하지 않을 경우 주문번호가 1234 인 데이터를 생성한 뒤 orders/1234 를 식별자로 사용한다.

## RESTful

> [RESTful 자세히 보기](https://github.com/BAEKJungHo/restful_basic/wiki/RESTful)

### 안전성과 멱등성

#### 안전한 메서드

- 안전한 메서드(safe method) 란 서버 측의 상태 정보를 변경하지 않는 메서드를 가리키다. ex) GET v1/coffees/orders/1234
- GET, HEAD 와 같은 안전한 메서드는 캐시가 가능 하다. POST, PUT, DELETE 는 서버 리소스를 변경하므로 안전한 메서드가 아니다.

#### 멱등한 메서드

- 멱등한 메서드(idempotent method) 란 몇번을 호출되더라도 동일한 결과를 리턴하는 메서드를 의미한다.

GET 메서드는 여러 번 호출되더라도 동일한 리소스를 반환하므로 멱등한 메서드이며, PUT 은 동일한 리소르를 업데이트 하므로 멱등한 메서드이다. DELETE 는 한 번 삭제하고 나면 더이상 리소스가 존재하지 않으므로 여러번 호출되더라도 결과가 같으므로 멱등한 메서드이다. POST 는 복수 호출 시 각기 다른 결과가 리턴되거나 새로운 리소스가 생성되므로 멱등하지 않다.

#### 기타 메서드

- HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

## 클라이언트에서 서버로 데이터 전송

데이터 전달 방식은 크게 2가지 이다.

- `쿼리 파라미터를 통한 데이터 전송`
  - GET
  - 검색, 정렬 등
- `메시지 바디를 통한 데이터 전송`
  - POST, PUT, PATCH
  - 회원 가입, 상품 주문, 리소스 등록, 리소스 변경
  
아래와 같은 4가지 상황이 있다.

- `정적 데이터 조회`
  - 이미지, 정적 텍스트 문서
- `동적 데이터 조회`
  - 주로 검색, 게시판 목록에서 정렬 필터(검색어)
- `HTML Form 을 통한 데이터 전송`
  - 회원 가입, 상품 주문, 데이터 변경
- `HTTP API 를 통한 데이터 전송`
  - 회원 가입, 상품 주문, 데이터 변경
  - 서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)
  
#### 정적 데이터 조회

/static/star.jpg 처럼 쿼리 파라미터를 사용하지 않고 GET 방식으로 단순하게 조회할 수 있다.

#### 동적 데이터 조회

```
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

쿼리 파라미터를 기반으로 정렬 필터에서 결과를 동적으로 생성한다.

- 주로 검색, 게시판 목록에서 정렬 필터(검색어)
- 조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용
- 조회는 GET 사용
- GET은 쿼리 파라미터 사용해서 데이터를 전달

#### HTML Form 데이터 전송

![img](/images/15.JPG)

![img](/images/16.JPG)

- HTML Form submit 시 POST 전송
  - 예) 회원 가입, 상품 주문, 데이터 변경
- Content-Type: application/x-www-form-urlencoded 사용
  - form 의 내용을 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)
- 전송 데이터를 url encoding 처리
  - 예) abc김 -> abc%EA%B9%80
- HTML Form 은 GET 전송도 가능
- Content-Type: multipart/form-data
  - 파일 업로드 같은 바이너리 데이터 전송시 사용
  - 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능(그래서 이름이 multipart)
  
#### HTTP API 데이터 전송

- 서버 to 서버
  - 백엔드 시스템 통신
- 앱 클라이언트
  - 아이폰, 안드로이드
- 웹 클라이언트
  - HTML에서 Form 전송 대신 자바 스크립트를 통한 통신에 사용(AJAX)
  - 예) React, VueJs 같은 웹 클라이언트와 API 통신
- POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송
- GET: 조회, 쿼리 파라미터로 데이터 전달
- `Content-Type: application/json을 주로 사용 (사실상 표준)`
  - TEXT, XML, JSON 등등

## HTTP API 컬렉션과 스토어, HTML FROM

크게 설계 방식은 다음과 같다.

- `HTTP API 방식`
  - 컬렉션(Collection) 방식 : POST 기반 등록, 서버가 리소스 URI 를 결정
  - 스토어(Store) 방식 : PUT 기반 등록, 클라이언트가 리소스 URI 를 결정
- `HTML FORM 방식`
  - 순수 HTML + HTML form 사용
  - GET, POST 만 지원
    - 따라서 한계가 있기 때문에 리소스 URI(ex. /members)에 동사로된 URI 를 추가(컨트롤 URI)해서 관리한다.

위에서 배웠듯이 POST 와 PUT 은 등록이 가능하다고 배웠다. HTTP API 를 설계할 때 이 둘의 차이를 잘 알아야하는데 지금부터 배워보자.

### HTTP API 컬렉션

컬렉션은 `POST 기반 등록`을 의미한다.

```
- 회원 목록 /members -> GET
- 회원 등록 /members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 /members/{id} -> PATCH, PUT, POST
- 회원 삭제 /members/{id} -> DELETE
```

- 클라이언트는 등록될 리소스의 URI 를 모른다.
  - 회원 등록 /members -> POST
  - POST /members
- 서버가 새로 등록된 리소스 URI를 생성해준다.
  - HTTP/1.1 201 Created
  - Location: /members/100
- `컬렉션(Collection)`
  - 서버가 관리하는 리소스 디렉토리
  - 서버가 리소스의 URI 를 생성하고 관리
  - 여기서 컬렉션은 /members
  
### HTTP API 스토어

스토어는 `PUT` 기반 등록을 의미한다.

```
- 파일 목록 /files -> GET
- 파일 조회 /files/{filename} -> GET
- 파일 등록 /files/{filename} -> PUT
- 파일 삭제 /files/{filename} -> DELETE
- 파일 대량 등록 /files -> POST
```

- 클라이언트가 리소스 URI 를 알고 있어야 한다.
  - 파일 등록 /files/{filename} -> PUT
  - PUT /files/star.jpg
- `클라이언트가 직접 리소스의 URI 를 지정한다.`
- `스토어(Store)`
  - 클라이언트가 관리하는 리소스 저장소
  - 클라이언트가 리소스의 URI를 알고 관리
  - 여기서 스토어는 /files

> 거의 POST 방식을 사용하고 PUT 방식은 사용을 거의 안하는데, 하는 경우가 있긴있다. 파일 업로더 같은 경우는 이 방식을 사용하기도 한다.
최근에 회사에서 소상공인 나눔터 홈페이지를 만드는데 동영상 솔루션이 들어와서 동영상 등록할 때 syncno 라는 키값을 서버에서 생성해서 
파일 업로드시 같이 넘기는데, 아마 동영상 솔루션 등록 방식이 `HTTP API 스토어` 즉, PUT 방식이지 않을까 싶다.
  
### HTML FORM

HTML FROM 은 `GET 과 POST 메서드만 지원`한다.

- AJAX 같은 기술을 사용해서 해결 가능 -> 회원 API 참고
- 여기서는 순수 HTML, HTML FORM 이야기
- GET, POST 만 지원하므로 제약이 있음

```
- 회원 목록 /members -> GET
- 회원 등록 폼 /members/new -> GET
- 회원 등록 /members/new, /members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 폼 /members/{id}/edit -> GET
- 회원 수정 /members/{id}/edit, /members/{id} -> POST
- 회원 삭제 /members/{id}/delete -> POST
```

- `컨트롤 URI`
  - GET, POST 만 지원하므로 제약이 있음
  - 이런 제약을 해결하기 위해 `동사로 된 리소스 경로 사용`
  - POST 의 /new, /edit, /delete 가 컨트롤 URI
  - HTTP 메서드로 해결하기 애매한 경우 사용(HTTP API 포함)
  
> 실무에서는 최대한 리소스라는 개념을 활용해서 URI 를 설계하고, HTTP 메서드로 해결하기 애매한 경우에 컨트롤 URI 를 사용하는 것이 좋다.

#### 정리

- `문서(document)`
  - 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
  - 예) /members/100, /files/star.jpg
- `컬렉션(collection)`
  - 서버가 관리하는 리소스 디렉터리
  - 서버가 리소스의 URI를 생성하고 관리
  - 예) /members
- `스토어(store)`
  - 클라이언트가 관리하는 자원 저장소
  - 클라이언트가 리소스의 URI를 알고 관리
  - 예) /files
- `컨트롤러(controller), 컨트롤 URI`
  - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
  - 동사를 직접 사용
    - 예) /members/{id}/delete
    - 예) /users/moveUp, /users/moveDown

## HTTP 상태 코드

### 1xx (Informational): 요청이 수신되어 처리중 (거의 사용 안함)

### 2xx (Successful): 요청 정상 처리

- 200 OK
- 201 Created 
  - 요청 성공해서 새로운 리소스가 생성됨
  - 생성된 리소스는 응답의 Location 헤더 필드로 식별한다.
- 202 Accepted
  - 요청이 접수되었으나 처리가 완료되지 않았음
  - 배치 처리 같은 곳에서 사용
  - 예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함
- 204 No Content
  - 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
  - 예) 웹 문서 편집기에서 save 버튼
  - save 버튼의 결과로 아무 내용이 없어도 된다.
  - save 버튼을 눌러도 같은 화면을 유지해야 한다.
  - 결과 내용이 없어도 204 메시지(2xx)만으로 성공을 인식할 수 있다.
  
![img](/images/17.JPG)
  
### 3xx (Redirection): 요청을 완료하려면 추가 행동이 필요

- 300 Multiple Choices
- 301 Moved Permanently
- 302 Found
- 303 See Other
- 304 Not Modified
- 307 Temporary Redirect
- 308 Permanent Redirect

> 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)

![img](/images/18.JPG)

- 리다이렉션 종류
  - 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동
    - 예) /members -> /users
    - 예) /event -> /new-event
  - 일시 리다이렉션 - 일시적인 변경
    - 주문 완료 후 주문 내역 화면으로 이동
    - `PRG: Post/Redirect/Get`
  - 특수 리다이렉션
    - 결과 대신 캐시를 사용

#### 영구 리다이렉션(301, 308)

- 리소스의 URI가 영구적으로 이동
- 원래의 URL를 사용X, 검색 엔진 등에서도 변경 인지
- 301 Moved Permanently
  - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- 308 Permanent Redirect
  - 301과 기능은 같음
  - 리다이렉트시 요청 메서드와 본문 유지(처음 POST를 보내면 리다이렉트도 POST 유지)
  
![img](/images/19.JPG)

![img](/images/20.JPG)
  
#### 일시작인 리다이렉션(302, 307, 303)

- 리소스의 URI가 일시적으로 변경
- 따라서 검색 엔진 등에서 URL을 변경하면 안됨
- 302 Found
  - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- 307 Temporary Redirect
  - 302와 기능은 같음
  - 리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다. MUST NOT)
- 303 See Other
  - 302와 기능은 같음
  - 리다이렉트시 요청 메서드가 GET으로 변경
  
`PRG: Post/Redirect/Get`

- POST로 주문후에 웹 브라우저를 새로고침하면?
- 새로고침은 다시 요청
- 중복 주문이 될 수 있다  

따라서 PRG 를 사용하여 아래와 같이 할 수 있다.

- POST로 주문후에 새로 고침으로 인한 중복 주문 방지
- POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트
- 새로고침해도 결과 화면을 GET으로 조회
- 중복 주문 대신에 결과 화면만 GET으로 다시 요청

![img](/images/21.JPG)

#### 302, 307, 303 중에 뭘 써야 할까?

- 302 Found -> GET으로 변할 수 있음
- 307 Temporary Redirect -> 메서드가 변하면 안됨
- 303 See Other -> 메서드가 GET으로 변경

- 역사
  - 처음 302 스펙의 의도는 HTTP 메서드를 유지하는 것
  - 그런데 웹 브라우저들이 대부분 GET으로 바꾸어버림(일부는 다르게 동작)
  - 그래서 모호한 302를 대신하는 명확한 307, 303이 등장함(301 대응으로 308도 등장)
- 현실
  - 307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 302를 기본값으로 사용
  - 자동 리다이렉션시에 GET으로 변해도 되면 그냥 302를 사용해도 큰 문제 없음

### 4xx (Client Error): 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음

- 클라이언트의 요청에 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 오류의 원인이 클라이언트에 있음
- 중요! 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패함

#### 400 Bad Request

클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음

- 요청 구문, 메시지 등등 오류
- 클라이언트는 요청 내용을 다시 검토하고, 보내야함
- 예) 요청 파라미터가 잘못되거나, API 스펙이 맞지 않을 때

#### 401 Unauthorized

클라이언트가 해당 리소스에 대한 인증이 필요함

- 인증(Authentication) 되지 않음
- 401 오류 발생시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명
- 참고
  - 인증(Authentication): 본인이 누구인지 확인, (로그인)
  - 인가(Authorization): 권한부여 (ADMIN 권한처럼 특정 리소스에 접근할 수 있는 권한, 인증이 있어야 인가가 있음)
  - 오류 메시지가 Unauthorized 이지만 인증 되지 않음 (이름이 아쉬움)
  
#### 403 Forbidden

서버가 요청을 이해했지만 승인을 거부함

- 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
  - 예) 어드민 등급이 아닌 사용자가 로그인은 했지만, 어드민 등급의 리소스에 접근하는 경우
  
#### 404 Not Found

요청 리소스를 찾을 수 없음

- 요청 리소스가 서버에 없음
- 또는 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때


### 5xx (Server Error): 서버 오류, 서버가 정상 요청을 처리하지 못함

- 서버 문제로 오류 발생
- 서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있음(복구가 되거나 등등)

#### 500 Internal Server Error

서버 문제로 오류 발생, 애매하면 500 오류

> 실무에서 서버에서는 가급적 500 Error 를 만들면 안된다. 500 Error 는 진짜 서버에 문제가 있는 경우에만 해야한다.
예를들어 클라이언트에서 값을 요청 메시지에 담아서 보내는데 그 값이 잘못된것이어서 서버에서 처리할 수 없고, 클라이언트가 그 값으로 
재요청해도 실패할 결과라면 클라이언트 오류 400 Error 로 만들어야한다. 500 Error 는 서버에 문제가 생겨서 클라이언트가 보냈던 요청 메시지를
다시 보내도 서버가 복구되면 성공할 가능성이 있다. 
>
> 예를들어 회원 잔고가 부족해서 서버에서 처리할 수 없는 경우 등 비지니스 로직 예외 케이스가 생기는 경우 클라이언트 에러로 처리해야한다.
그래서 나중에 모니터링을 할 때 500 Error 가 발생하면 서버에 심각한 문제가 생겼다는 것을 바로 알 수 있다.
>
> 즉, 500 Error 는 쿼리문제나, DB 가 내려가거나, NPE 나, 비지니스 로직 자체가 문제가 있는 경우 해당 에러를 발생시켜야한다. 그리고 나머지는 400 이랑 200 으로 해결해야한다.

#### 503 Service Unavailable

서비스 이용 불가

- 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
- Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음

### 만약 모르는 상태 코드가 나타나면 ?

클라이언트가 인식할 수 없는 상태코드를 서버가 반환하면?

- 클라이언트는 상위 상태코드로 해석해서 처리
- 미래에 새로운 상태 코드가 추가되어도 클라이언트를 변경하지 않아도 됨
  - 예)
    - 299 ??? -> 2xx (Successful)
    - 451 ??? -> 4xx (Client Error)
    - 599 ??? -> 5xx (Server Error)

## HTTP 헤더

- HTTP 표준
  - 1999 년 RFC2616 현재는 폐기됨
  - 2014 년 RFC7230 ~ 7235 등장
  
- RFC723X 변화
  - 엔티티(Entity) > 표현(Representation)
  - Representation = representattion Metadata + Representation Data
  - 표현 = 표현 메타데이터 + 표현 데이터
  
![img](/images/22.JPG)

### 표현

- Content-Type: 표현 데이터의 형식
  - text/html; charset=utf-8
  - application/json
  - image/png
- Content-Encoding: 표현 데이터의 압축 방식
  - 표현 데이터를 압축하기 위해 사용
  - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
  - 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
  - gzip
  - deflate
  - identity
- Content-Language: 표현 데이터의 자연 언어
  - ko
  - en
  - en-US
- Content-Length: 표현 데이터의 길이
  - 바이트 단위
  - Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

### 협상(Contents negotiation)

클라이언트가 선호하는 표현 요청

- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어

협상 헤더는 요청시에만 사용

## 일반 정보

- From: 유저 에이전트의 이메일 정보
  - 일반적으로 잘 사용되지 않음
  - 검색 엔진 같은 곳에서, 주로 사용
  - 요청에서 사용
- Referer: 이전 웹 페이지 주소
  - 현재 요청된 페이지의 이전 웹 페이지 주소
  - A -> B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청
  - Referer를 사용해서 유입 경로 분석 가능
  - 요청에서 사용
  - 참고: referer는 단어 referrer의 오타
- User-Agent: 유저 에이전트 애플리케이션 정보
  - user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/
537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
  - 클리이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
  - 통계 정보
  - 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
  - 요청에서 사용
- Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보
  - Server: Apache/2.2.22 (Debian)
  - server: nginx
  - 응답에서 사용
- Date: 메시지가 생성된 날짜
  - Date: Tue, 15 Nov 1994 08:12:31 GMT
  - 응답에서 사용
  
## 특별한 정보

- Host: 요청한 호스트 정보(도메인)
  - 요청에서 사용
  - 필수
  - 하나의 서버가 여러 도메인을 처리해야 할 때
  - 하나의 IP 주소에 여러 도메인이 적용되어 있을 때
- Location: 페이지 리다이렉션
  - 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
  - 응답코드 3xx에서 설명
  - 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
  - 3xx (Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴
- Allow: 허용 가능한 HTTP 메서드
  - 405 (Method Not Allowed) 에서 응답에 포함해야함
  - Allow: GET, HEAD, PUT
- Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
  - 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
  - Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
  - Retry-After: 120 (초단위 표기)
  
## 인증

- Authorization: 클라이언트 인증 정보를 서버에 전달
  - Authorization: Basic xxxxxxxxxxxxxxxx
- WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의
  - 401 Unauthorized 응답과 함께 사용
  - WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"
  
## 쿠키

- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

![img](/images/23.JPG)

![img](/images/24.JPG)

- 예) set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure
- 사용처
  - 사용자 로그인 세션 관리
  - 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
  - 네트워크 트래픽 추가 유발
  - 최소한의 정보만 사용(세션 id, 인증 토큰)
  - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고
- 주의!
  - 보안에 민감한 데이터는 저장하면 안됨(주민번호, 신용카드 번호 등등)
  
### 쿠키 생명 주기(Expires, max-age)

- Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
  - 만료일이 되면 쿠키 삭제
- Set-Cookie: max-age=3600 (3600초)
  - 0 이나 음수를 지정하면 쿠키 삭제
- 세션 쿠키 : 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지

### 쿠키 - Domain

- 예) domain=example.org
- 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
  - domain=example.org를 지정해서 쿠키 생성
    - example.org 는 물론이고
    - dev.example.org 도 쿠키 접근
- 생략: 현재 문서 기준 도메인만 적용
  - example.org 에서 쿠키를 생성하고 domain 지정을 생략
    - example.org 에서만 쿠키 접근
    - dev.example.org는 쿠키 미접근
    
### 쿠키 - Path

- 예) path=/home
- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 path=/ 루트로 지정
- 예)
  - path=/home 지정
  - /home -> 가능
  - /home/level1 -> 가능
  - /home/level1/level2 -> 가능
  - /hello -> 불가능
  
### 쿠키 - 보안(Secure, HttpOnly, SameSite)

- `Secure`
  - 쿠키는 http, https를 구분하지 않고 전송
  - Secure를 적용하면 https인 경우에만 전송
- `HttpOnly`
  - XSS 공격 방지
  - 자바스크립트에서 접근 불가(document.cookie)
  - HTTP 전송에만 사용
- `SameSite`
  - XSRF 공격 방지
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송
  
## 캐시

### 캐시가 없는경우

- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다.
- 인터넷 네트워크는 매우 느리고 비싸다.
- 브라우저 로딩 속도가 느리다.
- 느린 사용자 경험
  
### 캐시 적용

![img](/images/25.JPG)

![img](/images/26.JPG)

![img](/images/27.JPG)

![img](/images/28.JPG)

- 캐시 덕분에 캐시 가능 시간동안 네트워크를 사용하지 않아도 된다.
- 비싼 네트워크 사용량을 줄일 수 있다.
- 브라우저 로딩 속도가 매우 빠르다.
- 빠른 사용자 경험

따라서 조회와 같은 요청은 GET 을 사용해서 캐시를 사용하도록 하는게 훨씬 속도 측면에서도 좋다.

### 캐시 시간 초과

- 캐시 유효 시간이 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다.
- 이때 다시 네트워크 다운로드가 발생한다

캐시 유효 시간이 초과해서 서버에 다시 요청하면 다음 두 가지 상황이 나타난다.

1. 서버에서 기존 데이터를 변경함
2. 서버에서 기존 데이터를 변경하지 않음

- `캐시 만료후에도 서버에서 데이터를 변경하지 않음`
  - 생각해보면 데이터를 전송하는 대신에 저장해 두었던 캐시를 재사용 할 수 있다.
  - 단 클라이언트의 데이터와 서버의 데이터가 같다는 사실을 확인할 수 있는 방법 필요
  - `if-modified-since: 2020년 11월 10일 10:00:00 와 Last-Modified: 2020년 11월 10일 10:00:00` 를 비교해서 데이터가 수정되었는지 판단.
  
- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않으면
- 304 Not Modified + 헤더 메타 정보만 응답(바디X)
- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신
- 클라이언트는 캐시에 저장되어 있는 데이터 재활용
- 결과적으로 네트워크 다운로드가 발생하지만 용량이 적은 헤더 정보만 다운로드
- 매우 실용적인 해결책

### Last-Modified, If-Modified-Since 단점

- 1초 미만(0.x초) 단위로 캐시 조정이 불가능
- 날짜 기반의 로직 사용
- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
  - 예) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우
  
### ETag, If-None-Match

- ETag(Entity Tag)
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
  - 예) ETag: "v1.0", ETag: "a2jiodwjekjl3"
- 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)
  - 예) ETag: "aaaaa" -> ETag: "bbbbb"
- 진짜 단순하게 ETag만 보내서 같으면 유지, 다르면 다시 받기!
- 캐시 제어 로직을 서버에서 완전히 관리
- 클라이언트는 단순히 이 값을 서버에 제공(클라이언트는 캐시 메커니즘을 모름)
- 예)
  - 서버는 배타 오픈 기간인 3일 동안 파일이 변경되어도 ETag를 동일하게 유지
  - 애플리케이션 배포 주기에 맞추어 ETag 모두 갱신
  
### 캐시 헤더 제어

- Cache-Control: 캐시 제어
- Pragma: 캐시 제어(하위 호환)
- Expires: 캐시 유효 기간(하위 호환)

#### Cache-Control : 캐시 지시어(directives)

- Cache-Control: max-age
  - 캐시 유효 시간, 초 단위
- Cache-Control: no-cache
  - 데이터는 캐시해도 되지만, 항상 원(origin) 서버에 검증하고 사용
- Cache-Control: no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨(메모리에서 사용하고 최대한 빨리 삭제)
  
#### Pragma : 캐시 제어(하위 호환)

- Pragma: no-cache
- HTTP 1.0 하위 호환

#### Expires : 캐시 만료일 지정(하위 호환)

- expires: Mon, 01 Jan 1990 00:00:00 GMT
- 캐시 만료일을 정확한 날짜로 지정
- HTTP 1.0 부터 사용
- 지금은 더 유연한 Cache-Control: max-age 권장
- Cache-Control: max-age와 함께 사용하면 Expires는 무시

### 프록시 캐시

![img](/images/29.JPG)

![img](/images/30.JPG)

### 캐시 무효화

- Cache-Control: no-cache
  - 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용(이름에 주의!)
- Cache-Control: no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨(메모리에서 사용하고 최대한 빨리 삭제)
- Cache-Control: must-revalidate
  - 캐시 만료후 최초 조회시 원 서버에 검증해야함
  - 원 서버 접근 실패시 반드시 오류가 발생해야함 - 504(Gateway Timeout)
  - must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
- Pragma: no-cache
  - HTTP 1.0 하위 호환
  
#### no-cache

![img](/images/31.JPG)

![img](/images/32.JPG)

#### must-revalidate

![img](/images/33.JPG)

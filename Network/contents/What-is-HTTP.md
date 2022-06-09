# HTTP란?

1. [HTTP](#http)
2. [HTTP의 동작](#http의-동작)
3. [HTTP의 특징](#http의-특징)
   1. [HTTP의 간단한 예시](#http의-간단한-예시)
4. [요청(Request)](#요청request)
   1. [Request의 간단한 예시](#request의-간단한-예시)
   2. [요청의 종류(Request Method)](#요청의-종류request-method)
   3. [Request HTTP 메시지 예시](#request-http-메시지-예시)
      1. [시작줄(첫 줄)](#시작줄첫-줄)
      2. [헤더(두번째 줄부터)](#헤더두번째-줄부터)
      3. [본문(헤더에서 한 줄 띄고)](#본문헤더에서-한-줄-띄고)
5. [응답(Response)](#응답response)
   1. [Request의 간단한 예시](#request의-간단한-예시)
   2. [요청의 종류(Request Method)](#요청의-종류request-method)
   3. [Response HTTP 메시지 예시](#response-http-메시지-예시)
      1. [시작줄(첫 줄)](#ec8b9cec9e91eca484ecb2ab-eca484-1)
      2. [헤더(두번째 줄부터)](#ed97a4eb8d94eb9190ebb288eca7b8-eca484ebb680ed84b0-1)
      3. [본문(헤더 뒤부터)](#본문헤더-뒤부터)
6. [참고 자료](#참고-자료)

## HTTP

> HTTP(HyperText Transfer Protocol)은 텍스트 기반의 통신 규약으로, **인터넷에서 데이터를 주고받을 수 있는 프로토콜**이다.

인터넷 상에서는 이렇게 정해진 규약을 바탕으로 모든 프로그램에서 이 규약에 맞춰 통신하기 때문에 호환성 문제 없이 정보를 서로 교환할 수 있게 되었다.

## HTTP의 동작

HTTP는 클라이언트, 즉, 사용자가 브라우저를 통해서 특정 서비스를 URL이나 다른 수단을 통해 요청(Request)하면 서버에서는 해당 요청사항에 맞는 결과를 차장서 사용자에게 응답(Response)하는 형태로 동작한다.

- 요청 : Client → Server
- 응답 : Server → Client

HTTP 통신을 통해 주고받을 수 있는 정보에는 HTML 문서 외에도 다양하다. Plain Text부터 JSON, XML과 같은 형태의 정보도 주고받을 수 있으며, 보통은 클라이언트가 수신하는 정보를 어떤 형태(HTML, JSON 등)로 받지 싶은지를 명시하는 경우가 많다.

## HTTP의 특징

- HTTP 메시지는 HTTP 서버와 HTTP 클라이언트에 의해 해석된다.
- TCP/IP를 이용하는 응용 프로토콜이다.
- HTTP는 연결 상태를 유지하지 않는 비연결성 프로토콜이다.  
  (이 단점을 보완하기 위해 Cookie와 Session이 등장했다.)
- HTTP는 비연결성 프로토콜이기 때문에 요청/응답 방식으로 동작한다.

![HTTP-01](./images/HTTP-01.png)

### HTTP의 간단한 예시

- **서버** : 특정 자료에 대한 접근을 관리하는 네트워크 상의 시스템으로, **요청에 대한 응답을 보내준다.**
- **클라이언트** : 특정 자료에 접근할 수 있는 프로그램으로, 대표적으로 웹 브라우저가 있다.

클라이언트 프로그램에서 사용자가 회원가입을 시도할 경우, 서버로 회원정보가 전달되고 서버는 회원정보를 저장하기도 한다. 이 과정에서 **클라이언트와 서버 간의 교류가 HTTP라는 규약을 통해 이뤄진다.**

## 요청(Request)

> **클라이언트가 서버에게 연락하는 것**을 요청이라고 하며, 요청을 보낼 때는 요청에 대한 정보를 담아 함께 서버로 보낸다.

### Request의 간단한 예시

서버가 주문서를 받아 클라이언트가 무엇을 원하는지 파악할 수 있게 된다. 이처럼 **요청은 식당에서 주문서를 작성하는 것과 같다**고 생각하면 된다.

### 요청의 종류(Request Method)

- **GET** : 자료를 **요청**할 때 사용
- **POST** : 자료의 **생성**을 요청할 때 사용
- **PUT** : 자료의 **수정**을 요청할 때 사용
- **DELETE** : 자료의 **삭제**를 요청할 때 사용

### Request HTTP 메시지 예시

```http
GET https://www.google.com HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) ...
Upgrade-Insecure-Requests: 1
```

#### 시작줄(첫 줄)

첫 줄은 시작줄로 **메서드 구조 버전**으로 구성된다.

- GET : HTTP Method
- https://www.google.com : 사이트 주소
- HTTP/1.1 : HTTP 버전

#### 헤더(두번째 줄부터)

두번째 줄부터는 헤더이며, **요청에 대한 정보**를 담고 있다. `User-Agent`, `Upgrade-Insecure-Request` 등이 헤더에 해당되며 헤더의 종류는 매우 다양하다.

#### 본문(헤더에서 한 줄 띄고)

본문은 **요청을 할 때 함께 보낼 데이터를 담는 부분**이다. [상술한 예시](#request-http-메시지-예시)에서는 단순히 주소로만 요청을 보내고 있고, 별도의 데이터를 담아 보내지 않기 때문에 본문이 비어 있다.

## 응답(Response)

> **서버가 요청에 대한 답변을 클라이언트에게 보내는 것**을 응답이라고 한다.

### 상태 코드(Status Code)

상태 코드는 3자리 숫자로 구성되어 있으며, 첫번째 자릿수를 통해 크게 5가지로 구분된다.

- **1..(조건부 응답)** : 요청을 받았으며 작업을 계속 진행한다.
- **2..(성공)** : 클라이언트가 요청한 동작을 수신, 이해, 승낙했으며 성공적으로 처리했음을 나타낸다.
- **3..(리다이렉션 완료)** : 클라이언트가 요청을 마치기 위해 추가 작업이 필요함을 나타낸다.
- **4..(요청 오류)** : 클라이언트의 요청 문법이 잘못되었거나 요청 처리가 불가능함을 나타낸다.
- **5..(서버 오류)** : 서버가 유효한 요청을 명백하지 수행하지 못했음을 나타낸다.

### Response HTTP 메시지 예시

```http
HTTP/1.1 200 OK
Connection: keep-alive
Content-Encoding: gzip
Contnet-Length: 35653
Content-Type: text/html;

<!DOCTYPE html>
  <html lang="ko" data-reactroot="">
    <head>
      <title>
        ...
```

#### 시작줄(첫 줄)

첫 줄은 **버전 상태 코드 상태메시지**로 구성되어 있다. `200`은 성공적인 요청이었다는 의미다.

#### 헤더(두번째 줄부터)

두번째 줄부터는 헤더로 **응답에 대한 정보를 담고 있다.**

#### 본문(헤더 뒤부터)

응답에는 대부분의 경우 본문이 있다. 보통 데이터를 요청하고 응답 메시지에는 **요청한 데이터를 담아서 보내주기 때문이다. 응답 메시지에 HTML이 담겨 있는데 이 HTML을 받아 브라우저가 화면에 렌더링한다.**

## 참고 자료

- [HTTP란 무엇인가?](https://velog.io/@surim014/HTTP%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
- [HTTP 상태 코드 정리](https://brunch.co.kr/@leedongins/65)
먼저 HTTP 프로토콜의 특성이자 약점을 보완하기 위해서 쿠키 또는 세션을 사용합니다.

# HTTP(HyperText Transfer Protocol)

텍스트 기반의 통신 규약으로 인터넷에서 데이터를 주고받을 수 있는 프로토콜이다.

웹 페이지를 방문할 때마다 컴퓨터는 HTTP(Hypertext Transfer Protocol)를 사용하여 인터넷 어딘가에 있는 다른 컴퓨터에서 해당 페이지를 다운로드한다.

## HTTP 의 역사

**HTTP/0.9** : GET 메서드만 지원, HTTP 헤더 없음

**HTTP/1.0 **: 메서드, 헤더 추가(⇒ HTML 이외 다른 파일 전송 가능)

**HTTP/1.1** : 현재 HTTP/1.1 주로 사용, 우리에게 가장 중요한 버전

**HTTP/2** : 성능 개선

**HTTP/3** : 진행중, TCP 대신에 UDP 사용, 성능 개선

HTTP/1.1, HTTP/2는 TCP 기반이며 HTTP/3는 UDP 기반 프로토콜이다.

## HTTP 의 특성

- TCP/ IP를 이용하는 응용 프로토콜입니다.
  (컴퓨터와 컴퓨터간에 데이터를 전송 할 수 있도록 하는 장치로 인터넷이라는 거대한 통신망을 통해 원하는 정보(데이터)를 주고 받는 기능을 이용하는 응용 프로토콜)

- HTTP 프로토콜 환경은 "connectionless, stateless"한 특성을 가지기 때문에 서버는 클라이언트가 누구인지 매번 확인해야합니다. 이 특성을 보완하기 위해서 쿠키와 세션을 사용하게됩니다.

- HTTP는 연결을 유지하지 않는 프로토콜이기 때문에 요청/응답 방식으로 동작합니다.

### connectionless

클라이언트가 요청을 한 후 응답을 받으면 그 연결을 끊어 버리는 특징

### stateless

통신이 끝나면 상태를 유지하지 않는 특징

쿠키와 세션을 사용하지 않으면 쇼핑몰에서 옷을 구매하려고 로그인을 했음에도, 페이지를 이동할 때 마다 계속 로그인을 해야 합니다.

쿠키와 세션을 사용했을 경우, 한 번 로그인을 하면 어떠한 방식에 의해서 그 사용자에 대한 인증을 유지하게 됩니다.

# 🍪쿠키 ( Cookie )

- 쿠키는 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 작은 데이터 파일입니다.
- 사용자 인증이 유효한 시간을 명시할 수 있으며, 유효 시간이 정해지면 브라우저가 종료되어도 인증이 유지된다는 특징이 있습니다.
- 쿠키는 클라이언트의 상태 정보를 로컬에 저장했다가 참조합니다.
- 클라이언트에 300개까지 쿠키저장 가능, 하나의 도메인당 20개의 값만 가질 수 있음, 하나의 쿠키값은 4KB까지 저장합니다.
- Response Header에 Set-Cookie 속성을 사용하면 클라이언트에 쿠키를 만들 수 있습니다.
  쿠키는 사용자가 따로 요청하지 않아도 브라우저가 Request시에 Request Header를 넣어서 자동으로 서버에 전송합니다.

# 👨‍👨‍👧세션 ( Session )

- 세션은 쿠키를 기반하고 있지만, 사용자 정보 파일을 브라우저에 저장하는 쿠키와 달리 세션은 서버 측에서 관리합니다.
- 서버에서는 클라이언트를 구분하기 위해 세션 ID를 부여하며 웹 브라우저가 서버에 접속해서 브라우저를 종료할 때까지 인증상태를 유지합니다.
- 물론 접속 시간에 제한을 두어 일정 시간 응답이 없다면 정보가 유지되지 않게 설정이 가능 합니다.
- 사용자에 대한 정보를 서버에 두기 때문에 쿠키보다 보안에 좋지만, 사용자가 많아질수록 서버 메모리를 많이 차지하게 됩니다.
  즉 동접자 수가 많은 웹 사이트인 경우 서버에 과부하를 주게 되므로 성능 저하의 요인이 됩니다.
- 클라이언트가 Request를 보내면, 해당 서버의 엔진이 클라이언트에게 유일한 ID를 부여하는 데 이것이 세션 ID입니다.

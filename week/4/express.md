# Express

## Express란?

[express](https://expressjs.com/ko/)는 Node JS 기반의 서버 웹 프레임워크이다. 가볍고 간단하고 빠르게 설정할 수 있어 많이 사용한다.

다른 Node 기반 framework의 기반이 되기도 한다.

* GraphQL-yoga : 간단하고 경량의 graphQL 서버
* [NestJS](https://github.com/nestjs/nest) : 서버 사이드 앱 개발 프레임워크. Decorators,DI로 모듈화를 통한 재사용성, 확장성 증강. Express와 함께 사용 가능

### 사용 방법

* 포트번호 지정
* express 초기화
* rounting 설정. 특정 endpoint에 대해 어떤 응답을 할지 지정한다. method, path, handler가 한 세트로 있다.
  * Endpoint란? 끝점. 클라이언트가 API에 접근하기 위한 URL 주소. 둘 간 상호작용을 위한 인터페이스 역할을 한다고 볼 수 있다 .
* listen : 연결 요청을 받기 위해 포트 할당 및 대기한다.
* use : 특정 middleware 함수/path에 대한 함수를 mount 한다
  * middleware : 프로그램 요청-응답 사이에서 요청,응답을 다루거나 다른 기능을 제공하는 소프트웨어 구성 요소

#### mount - import ?

Web framework에서는 앱/라이브러리를 라우팅 경로에 연결해서 실행 가능하도록 하는 행위다. os 에서는 File system을 접근 가능하도록 등록하는 행위다. 뭉뚱그리면 별개의 대상을 접근해서 사용가능하도록 연결/등록하는 과정을 mount라 한다. mount는 올라탄다는 뜻이며, framework -> middleware, OS -> file system 관계에서 볼 수 있듯이 기반으로 하는 프로그램이 그 위에서 동작할 수 있는 프로그램을 사용하기 위해 얹는 과정으로 보인다.

그렇다면 import와는 어떤 차이가 있나 싶었다. import는 모듈을 다른 모듈에서 재사용하기 위해 가져오는 행위라면,  mount는 Web App을 미들웨어 함수에 연결해서 해당 기능을 사용할 수 있도록 하는 과정이다.

다 가져다 쓰는 재사용 가능한 것인데, 굳이 차이점을 나눈다고 한다면

* import : 보통 코드상에서 모듈을 사용할 때
* mount : middleware나 file system 같이 더 큰 규모의 프로그램을 사용할 때

로 나눌 수 있을 것 같다. 굳이... 굳이 비유하자면 import, export는 비행기 탈때 수화물을 떠올릴 수 있을 것 같다. mount는 컨테이너선에 컨테이너를 싣는 것과 비슷하다고 느꼈다.

## URL 구조

### URL 이란?

[URL(Uniform Resource Locator)](https://developer.mozilla.org/ko/docs/Learn/Common_questions/Web_mechanics/What_is_a_URL)은 웹에서 고유한 resource를 접근하기 위한 주소다.
URL 구조는
https://some-site.com:1231/menu?search=movie&option=none
```text
[Protocol]://[Domain][Port(option)] / [links and slashes] [? -> 이후에 query parameter가 온다][key=value -> 여러개가 올때는 & 로 구분]
```
- REST API

roy fielding이 박사논문으로 발표한, http 프로토콜 , 자원 기반의 웹 아키텍처 스타일이다. resource를 기반으로 해서 uri를 통해 자원을 명시하고, http method를 사용해서 자원에 대한 행위를 서술한다.

http의 가이드 제약 조건을 따르느냐에 따라서 level을 나눈 경우도 있는데, level 0는 http tunnel만 사용해서 원격 프로세스 실행하는 정도에 그친다. level 1은 resource를 uri에 명시하고, level 2는 자원에 대한 행위를 http method로 나타낸다(이전은 무조건 POST). level 3는 HATEOAS(Hypertext as the engine of application state)라고 해서 요청을 했을 때 응답 뿐만 아니라 해당 상태에서 다음에 어떤 자원을 요청할 수 있는지에 대한 사용 설명서를 하이퍼링크까지 친절하게 첨부해서 보내는 것이다.

- HTTP Method(CRUD)
자원은 item(단수) collection(복수)가 있다.

GET(READ) : 자원을 요청할 때 사용한다. 멱등적(idempotent)인데 이는 요청을 계속 반복해도 같은 결과를 받을 수 있다는 뜻이다.
POST(CREATE) : 자원을 서버 상에 생성할 때 사용한다. BODY 상에 만들고자 하는 자원을 같이 보내며, 멱등적이지 않다
PUT,PATCH(UPDATE) : PUT은 자원 전체를 갱신하고, PATCH는 자원의 일부만 갱신한다. PATCH는 이후에 제시되었으며, 요즘은 PUT 보다는 PATCH가 더 많이 쓰인다.
DELETE(DELETE) : 자원을 삭제한다. 근데 이렇게 자원을 요청만 보낸다고 다 지워버리는 것은 비가역적이기에 너무 위험할 것 같다. 안전성의 문제로 대부분 경우 비활성한다고 한다.

 DB에서의 경우 요청이 삭제일지라도 실제로 삭제를 하지는 않고 db table 상에서 delete flag를 true로 바꾸는 식으로 soft delete를 하고는 한다. 그래야 나중에 문제가 생겼을 경우 복구를 하던지 할 수 있다. 꼭 DB상의 record가 아니더라도 서버상의 모든 자원은 지울 때 신중해야 한다.

curl, http ( httpie 설치로 가능)
- Express 란

express는 Node JS 기반의 서버 웹 프레임워크이다. 가볍고 설정하기가 간편한 측면이 있어 많이 사용한다.

- URL 구조
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

# Routes

## 라우터란?

route는 길,노선, 항로; 수단; 보내다, 발송하다 ; 노선을 정하다 라는 뜻을 가지고 있다.

router를 뜻으로 정리해보면 주어진 input에 따라 정해둔 경로로 대상을 인도하는 역할을 한다고 볼 수 있다.

[Routers](https://developer.mozilla.org/en-US/docs/Glossary/Routers)

1. 네트워크 간 data packet을 전달하는 장치
2. [SPA](https://developer.mozilla.org/en-US/docs/Glossary/SPA)에서 URL을 통해 어떤 웹 페이지를 보여줄지 결정하는 라이브러리. 보통 middleware module이 해당 기능을 지원한다.
3. service 레이어 내, 요청을 받아서 적절한 핸들러로 요청을 전달하는 소프트웨어 구성요소.

[routes and controllers](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/routes)

![routes](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/routes/mvc_express.png)

## React Router

client side routing을 해주는 기능. server로 추가적인 요청 없이 URL/UI를 업데이트 할 수 있다.

### Browser Router

[BrowserRouter](https://reactrouter.com/en/main/router-components/browser-router)

browser의 내장 history stack과 clean URLs를 이용해서 브라우저 주소의 현재 위치를 저장한다.

### Route

[Route](https://reactrouter.com/en/main/route/route)

URL 세그먼트와 컴포넌트, 데이터 로딩 및 데이터 변형을 연결. route nesting(경로 중첩)을 통해 복잡한 레이아웃, 데이터 의존성을 간단, 선언적으로 만든다.

### Memory Router

[Memory Router](https://reactrouter.com/en/main/router-components/memory-router)

그 자신의 위치를 배열 형태로 내부에 저장한다. BrowserHistory, HashHistory와는 달리 외부 소스에 매여있지 않는다. browser history stack 처럼 testing 상황에서 완전하게 조종할 수 있다.

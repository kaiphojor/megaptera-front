# MSW

## Service worker

[Service Worker](https://developer.mozilla.org/ko/docs/Web/API/Service_Worker_API)는 Web App 과 브라우저 사이에서 작동하는 프록시 서버 역할 하는 스크립트

오프라인에서 온라인에서 하는 것 처럼 비슷하게 요청 처리를 하기 위해서 생겼다. 웹앱의 백그라운드에서 동작, 주로 네트워크 요청을 가로채서 처리한다.

주요 기능

* 네트워크 요청 가로채기 : 요청을 오프라인 상황에서도 임의로 캐시된 리소스로 처리
* 캐싱 : 오프라인에서 제공하기 위한 리소스 캐싱.
* 백그라운드 동기화 : 온라인 전환시 서버에 변경사항을 동기화 함
* 푸시 알림 : 알림 수신/처리해서 백그라운드에서 알림 표시

[Service Worker overview](https://developer.chrome.com/docs/workbox/service-worker-overview/)

### Worker

[worker](https://developer.mozilla.org/ko/docs/Web/API/Worker)는 스크립트로 생성하고 생성자와 메시지 통신 백그라운드 작업을 하기위한 인터페이스

### interface

어떠한 대상이 다른 대상과 상호작용하기 위해 정한 규약.

## MSW(Mock Service Worker)

[MSW](https://mswjs.io/) 는 클라이언트의 API 요청을 가로채서 가짜 응답을 반환 하는 가짜 서버를 제공하는 Javascript library 이다. 이를 통해 백엔드 의존성 없이 API test를 수행 할 수 있다.

MSW의 service worker는 웹 앱과 브라우저 사이에서 작동하는 중간 계층이다. MSW는 service worker의 기능을 활용해서 API 요청을 가로채서 가짜 응답을 제공한다.

그렇게 오프라인 환경에서도 테스트 시나리오를 구성해서 시뮬레이션할 수 있게 된다.

### MSW , 실제 server와의 차이

1. 서버 통신 여부 : 실제 server와는 달리 네트워크를 거치지 않고 MSW가 가로채서 처리해버린다.
2. 데이터 영속성 : 네트워크 통신이 안되니 MSW는 DB나 스토리지에 데이터를 저장하지 않는다. 네트워크 계층을 모방하는 세션이 지나면 데이터는 유지되지 않는다
3. 테스트 환경 : 실제 서버 환경과는 달리 예측가능한 요청/응답을 정해서 시뮬레이트한다.

## polyfill(폴리필)

fetch가 browser에서는 되는데 node에서는 동작안한다
window.fetch에서 되는 것을 node 에서는 github에서 만든 fetch polyfill whatwg-fetch 를 써준다.

[polyfill](https://developer.mozilla.org/ko/docs/Glossary/Polyfill) 은 최신 javascript 에서 지원하지만 구 버전 브라우저 에서 동작 안하는 기능을 동일하게 기능하도록 지원하는 라이브러리이다. polyfill 은 이전의 대상에서 지원안하는 많은 기능을(poly) 구현해서 채워준다(fill) 는 것에서 유래되었다.

polyfill을 다 구현해놓은 것이나 ponyfill은 필요한 것만 선택적으로 로드 할 수 있게 만들어서 번들링시 경량화를 할 수있다는 이점이 있다.

임시서버 express 까지는 아니지만 구색을 맞출수 있는 정도라면 msw가 적당하다.

polyfill은 API/메소드/속성을 빠진것을 보충해주는 역할이기에 기능 사용 이전에 load되어야만한다.

[polyfill.io](https://polyfill.io/v3/)

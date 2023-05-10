# MSW

service worker?

mock server worker

네트워크 레벨에서 작업 지원 가능한, node , browser 에서 쓰는 service worker. 오프라인작업을 위한 가능

polyfill

waitfor - 기다려준다

fetch가 browser에서는 되는데 node에서는 동작안한다
window.fetch에서 되는 것을 node 에서는 github에서 만든 fetch polyfill whatwg-fetch 를 써준다.

polyfill 은 현 버전에서 구현 안되고 다른 버전에서 구현된 함수를 현 버전상에서 동일하게 기능하도록 구현한 라이브러리이다. polyfill 은 polyglot(다중 언어) 상에서 구현 안된 함수를 구현해서 채워준다(fill) 하는 것으로 느껴졌다.

polyfill을 다 구현해놓은 것이나 ponyfill은 필요한 것만 선택적으로 로드 할 수 있게 만들어서 번들링시 경량화를 할 수있다는 이점이 있다.

임시서버 express 까지는 아니지만 구색을 맞출수 있는 정도라면 msw가 적당하다.

handler 쪽에서 관리가 가능해서 실제 쓰는 것처럼 작동을 할 수 있다.
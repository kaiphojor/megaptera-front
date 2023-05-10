# Playwright

## E2E(End to End) Test

종단간 테스트는 사용자 관점에서 시스템의 전체적인 흐름을 테스트하는 방식이다.

사용자 시나리오를 시뮬레이션해서 구성요소/서비스들이 잘 상호작용하는지를 확인한다. 사용자가 어플리케이션을 사용하면서 발생할 수 있는 문제를 테스트과정에서 미리 발견할 수 있다.

E2E 테스트는 코드가 예상대로 작동하는지 확인하고, 요구사항을 충족했는지도 검증하기 용이하다.

### E2E 관련 키워드

* Cypress : E2E 테스트를 위한 JS 기반 도구. Web App 테스트를 간편하게 작성 실행 가능
* Selenium : 다양한 언어를 지원하는 Web App 자동화 테스트 도구.
* Puppeteer : Headless chrome/chromium 이용해 web browser 자동화를 하는 Node 라이브러리.

## Headless Chrome

[Headless Chrome](https://developer.chrome.com/blog/headless-chrome/)은 chrome browser의 headless 모드이다.

```text
headless mode : UI(창)없이 작동. 브라우저 창을 없이 웹페이지 렌더링/조작 가능한 기능.
```

자동화 web test, web scraping, SSR 등의 작업이 가능하다

## Puppeteer

크롬 팀에서 개발한 [Node Library](https://pptr.dev/). (headless) chrome 에 대한 고수준 API를 제공한다.

스크린샷, pdf, 웹스크래핑,폼 작성, 사용자 상호작용, 브라우저 테스트를 자동화하는데 유용하다.

## Playwright

Web App의 테스트 자동화를 제공하는 JS library. puppeteer 처럼 headless chrome 제어. puppeter에서 영향 받음

특징

* 여러 브라우저 지원(Headless Firefox, WebKit - Safari)
* 여러 언어 지원(JS,TS,Python,C#)
* 다중 탭 및 프레임 관리
* 사용이 용이한 API

## CodeceptJS

[CodeceptJS](https://codecept.io/)는 웹 E2E 테스트를 위한 JS 기반 프레임워크입니다.

* 구어체 - 일반인이 쓰는 자연어로 된 가독성 좋은 테스트 함수. 비개발자와 코드를 보면서 소통하기 좋음
* 다양한 드라이버- Playwright, Puppeteer 통해 test를 돌릴 수 있음. 뭐가 오던 코드는 똑같음
* 테스트 자동화 : 웹 앱과 상호작용(클릭, 입력)등을 지원
* 풍부한 검증 라이브러리

# React Component

- REST API 와 GraphQL
    - REST API 란 무엇인가
    - GraphQL은 왜 등장했는가?
    - REST API vs GraphQL

## REST API

### REST API 란?

#### 최초언급

REST 최초정의는 roy fielding의 박사논문 에서 언급되었다.

[Architectural Styles and the Design of Network-based Software Architectures](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)

최초정의 - REST architecture style : 복잡하고 분산된 시스템을 구성하기 위한 추상화한 아키텍처 스타일. component 역할/ 상호작용시 제약조건 / 중요 data element 해석에 집중하려고 component 구현/ protocol 구문 세부사항은 일부러 무시함

-> 그렇기에 보면 큰 그림에서 REST 방식은 어떻게 돌아가는지 정도만 나타나 있지 다른 언어나 framework의 docs처럼 공식 문서의 문법에 대한 딱 정해진 세부사항은 없는 듯 하다.

제약사항 - 해당 제약사항을 통해 간단하고, 확장성, 가시성, 사용성을 확보한 웹 서비스 구성이 가능하다. HTTP 저자가 만들었기에 http 특성도 일부 있다.

* 클라이언트 - 서버 아키텍처 스타일 - UI 관심사와 데이터 관심사를 분리하는 관심사의 분리가 핵심. 분리를 하면 플랫폼 별 UI 이식성 향상 및 서버 확장성도
꾀할 수 있다.

* 무상태 - 요청시에 모든 정보를 담아야 하며 이전 요청의 맥락 그런건 기대하면 안된다. 이전에 보냈던 정보를 똑같이 담아야하는 트레이드 오프는 있지만, 가시성(요청 관련 정보를 다 보내므로), 확장성(상태 저장 안해서 자원 해제가 용이) 측면에서 감수할만하다.
-> 확장성에 대해서 언급하자면, 상태, 즉 컨텍스트를 가진다는 것은 그 맥락을 서버 전체가 가지고 있어야 한다는 것과 동일하다. 그렇지 않으면 이전 요청을 받았던 서버만 응답이 가능하기에 서비스가 되지 않는다. 서버가 1대라고 가정하면 상관이 없을 것이다. 하지만 서버가 늘어날 수 있는 가능성(확장성)을 고려하면 무상태 방식으로 가는 것이 요청의 중복이 일어날 지언정 더 적절하다고 본다. 가시성은 말 그대로 이전 요청의 상태(컨텍스트)를 허용한다면 암묵적인 정보가 해당 요청시에 들어가게 되므로 보이지 않기에 나온 것이다. 무상태 서버 에서는 요청 처리에 필요한 모든 정보가 명시적으로 드러나기에 가시성 면에서 상태 서버 방식보다 낫다 .

* 캐시 - 이전 응답 정보 중 재사용할만한 것들을 캐시로 저장해서 재활용하면 자원 낭비를 안해도 되어서 효율적이고 사용성도 좋아진다.
-> 똑같은 요청을 계속 보내는데 그 요청이 GET 처럼 멱등적이라면 굳이 일일이 서버의 자원을 요청할 필요가 없는 것 처럼 말이다. 그리고 똑같은 것을 굳이 가져온다고 쳐도 클라이언트 - 서버 간 네트워크를 통해서 받아오는 것 보다 클라이언트 상의 브라우저 캐시에 접근해서 가져오는 것이 속도면에서 훨씬 빠르고 말이다. 물론 이것은 가져오는 자원이 급격하게 변하지 않는다는 전제에서 성립한다.

* 균일한 인터페이스 - component 간 통합 인터페이스 때문에 더 간단해지고 상호작용하는것도 더 가시적이다. 서비스 별 분리되어 있기에 독립적으로 발전 가능하다. 정보 전달시 해당 상황에 필요없는 정보도 표준화된 규격에 맞춰서 보내야 한다는 점은 비효율적이나(trade off), 대용량 하이퍼미디어 전송을 용이하게 해주므로 어느정도 감수할만하다.

* 계층적(layered) 시스템 - 계층으로 나누면 컴포넌트에서 상호작용하는 맞닿은 계층 너머의 정보를 알 수 없다. 서비스 접근도 선별적으로 통제하는 등 component 관리도 간단하게 할 수 있다.
-> 계층이 많이 나뉘면 그에 따른 오버헤드 및 성능저하도 생기나, 캐시 사용으로 충당이 가능하다고 여겼던 것 같다. 통합 인터페이스 또한 대용량 파일들을 웹으로 처리하기 용이하게 최적화되어 있어 실제로 웹 사용시에 이로인한 큰 불편을 느끼지는 못한다.

선택 제약 조건(Optional)

* code-on-demand : 클라이언트 상에서 script 코드 다운 혹은 실행을 가능하게끔 허용한다. 이렇게 클라이언트 쪽 기능 확장을 가능하게하면, 확장성을 고려해서 클라이언트 기능을 처음에 간단하게 구성할 수 있다. 나중에 시스템을 충분히 확장할 수 있으니 말이다.

#### AWS 문서

[AWS - RESTful API](https://aws.amazon.com/ko/what-is/restful-api/)

정의 - API 작동 방식에 대한 조건(제약사항)을 걸어주는 SW architecture이다. REST를 통해 대규모 통신을 안정적으로 할 수있게끔 방향성과 제약사항이 제시되었다. 해당 아키텍처를 따라 설계한 API를 REST(ful) API라 하고 REST 아키텍처를 구현한 web 서비스를 RESTful web 서비스라고 한다.

인터페이스 원칙

1. 자원의 식별 : 요청이 리소스를 식별해야 한다. 그러기 위해 균일한 리소스 식별자를 사용한다.
2. 메시지를 통한 리소스의 조작 : 클라이언트는 리소스를 수정/삭제할 수 있는 충분한 정보가 담긴 resource representation를 받아야 한다. 그러기 위해 서버는 리소스 관련 메타데이터를 보낸다.
3. 자기서술적 메시지 : 클라이언트는 표현을 추가 처리할 수 있는 정보를 받아야한다. 그러기 위해 서버는 리소스를 적절하게 사용하는 방법 관련 메타데이터가 담긴 메시지를 보내야한다. -> 표현이 표현을 사용하는 방법을 같이 보내는 것은 간단히 말하면 나 사용 설명서이다.
4. 애플리케이션 상태에 대한 엔진으로서 하이퍼미디어 : 클라이언트는 작업을 완료하는 데 필요한 기타 리소스 관련 정보를 받아야 한다. 그러기 위해 서버는 representation에 하이퍼링크를 넣어서 추가 리소스를 동적으로 검색할 수 있게 한다.

RESTful API의 이점

1. 확장성
2. 유연성 - 클라이언트 서버 분리를 통한 독립적인 발전이 가능. roy fielding 은 이것을  independent evolvability(독립적인 진화가능성) 이라고 언급한다.
3. 독립성 - REST API는 사용 기술과 독립적이기에 프로그래밍 언어에 구애받지 않는다.

### GraphQL은 왜 등장했는가?

#### GraphQL이 뭔가?

API를 위한 쿼리 언어이자, 기존 데이터로 해당 쿼리 수행하기 위한 기반 런타임이다. API의 데이터에 대한 완벽하고 이해가능한 설명을 제공한다. 그리고 필요로 하는 데이터만 정확히 질의 가능하다. 기존 query에 영향을 끼치지 않고 새 field/type을 추가하는 것(버전 없이 API 발전)이 가능하다. 그리고 강력한 개발자 도구를 제공한다.

data를 정의하는 type system을 이용하는 server side runtime이다. GraphQL은 DB나 storage engine에 연결되지 않고 코드/ 데이터에 의해 지원받는다.

### REST API vs GraphQL

모두 클라이언트와 서버 간의 통신을 위한 웹 API 지만 차이가 있다.

REST API는 HTTP 프로토콜의 구조와 제약 사항을 따르는 아키텍처 스타일입니다. REST API는 자원(resource)을 중심으로 설계되며, 자원을 URI(Uniform Resource Identifier)로 나타내고, 자원에 대한 행위는 HTTP 메소드(GET, POST, PUT, DELETE 등)를 사용하여 표현합니다. REST API는 네트워크 캐싱, 스케일링, 로드 밸런싱 등의 이점을 제공하지만, 복잡한 데이터 구조를 처리하기 어려운 단점이 있습니다.

GraphQL은 Facebook에서 개발한 쿼리 언어 및 런타임입니다. GraphQL은 REST API의 단점을 보완하고, 클라이언트 측에서 쿼리를 작성하고, 서버 측에서 응답을 생성하는 방식으로 동작합니다. GraphQL은 클라이언트가 필요로 하는 데이터를 정확하게 요청할 수 있도록 해주며, 서버 측에서는 클라이언트의 요청에 대해 필요한 데이터만을 반환합니다. GraphQL은 복잡한 데이터 구조를 다루는 데 유용하며, 클라이언트 측에서 쿼리를 작성하는 데에는 높은 학습 곡선이 필요합니다.

|                | **REST API** | **GraphQL**|
|:---:|:---:|:---:|
| 정의 | REST API는 자원 중심의 아키텍처 스타일 | GraphQL은 데이터 중심의 쿼리 언어 |
| 무엇을 하는가 | REST API는 HTTP 메소드를 사용, 자원에 대한 행위를 나타냄 | GraphQL은 단일 엔드포인트를 사용, 클라이언트에서 요청하는 데이터 처리 |
| 통신  | HTTP 통한 Client - server 통신 | HTTP,Web Socket 통한 Client - server 통신 |
| READ | RESTful 엔드포인트는 고정 데이터 구조 반환              |  클라이언트가 쿼리를 통해 특정 데이터를 요청할 때 그 데이터에 상응하는 구조 반환             |
| Updates   | HTTP 메소드 이용(PUT, POST, DELETE) | mutation 이용한 데이터 변경          |
| return Data 형태     | Endpoint 가 결정          | Client 가 결정            |
| 캐시가능        | RESTful API 는 endpoint 단계에서 캐시가능하다 | GraphQL response 는 endpoint 단계에서 캐시 불가 |
| Overfetching(과한 데이터 가져오기)  | RESTful APIs는 불필요한 데이터도 균일한 인터페이스 제약 조건 때문에 종종 포함된다.             | GraphQL queries는 오직 필요한 데이터만 요청 |
| Underfetching(API 요청 하나로 부족) | RESTful API 는 필요 데이터를 위해 추가요청 필요할수도 | GraphQL query 는 한 요청에 필요한 모든 데이터 가져오기 가능 |
| 스키마         | 필요없음                          | GraphQL API는 type / field 정의 위한 스키마 필요     |


BE에서 JSON 형태 데이터를 돌려주는 API를 제공한다고 가정하면 대부분은 REST API 또는 GRAPHQL 이다

rest api - GET, POST, PUT/PATCH , DELETE(CURD).
Resource 중심

GRAPHQL

- graph 자료구조
- query에서 얻고자 하는 것을 스키마처럼 지정
- query(읽기), mutation(Command: CUD), Subscription(Event 인지 용도. command 관련)

## State 란?

한 화면 UI를 나눈 조각이 Component라면, Component는 특정 상태에 따라 표시하는 부분이 달라질 수 있다. component를 변화를 결정하는 가변적인 상태를 React의 State이다.

### step by step

- UI 간단하게 component로 나눠보기 - UI를 컴포넌트 계층구조로 나누기
- component hierarchy 정하기
- 데이터 모델을 렌더링한 정적인 버전 제작하기(노가다) . 간단한 프로젝트 top down 대규모 프로젝트 bottom up
이때 props는 데이터 전달용으로 쓰는데, state는 상호작용성을 위한 것이므로 정적인 react코드 작성시에는 추가하지 않는다 .
오직 jsx 리턴. props tow down 방식 전달

상황별 UI를 모두 보여주는 최소한의 UI State 정의
state 아닌것

- 불변하는 것 - 상태가 가변적인 것을 상정하는데 불변하면 Nonsense
- props 통해 부모 component에게서 전달됨 - 그럼 props이지 state 아님.
- state/ props로 계산 가능 - '최소한의 정의'를 위반함

판별 결과

- product list - props로 전달되는 것
- 검색어/ checkbox - state.
- filtered list - 계산 되는 것

어느 component에서 state 변경을 책임질 지 정하기(소유할 component 정하기)

- state 사용하는 component 찾기 -> 공동 부모 찾기 -> 어디에 state를 관리할지 정하기
정해서 부모 component일 경우 props 처럼 내려 보낸다 .

### SSOT가 나온 이유는? state와의 관계는 ?

데이터는 딱 한곳에서 제어, 조작하는 정보모델이 SSOT(Single Source of Truth) 이다. 현실세계에서 국민의 의료정보를 한곳에서 통합관리하고 각 병원에서 이걸 참조하는 사례도 이 모델에 해당한다.

State도 마찬가지다. 같은 state를 여러 군데에서 독자적으로 중구난방 사용하면 관리가 제대로 안된다. 만약 독자적인 state가 있고 이것을 모두 동기화 해준다면 일일이 업데이트를 해줘야 하니 state를 이용하는 과정보다 state 동기화 하는 과정이 더 많이 걸리게 될 수도 있다. 그렇게 보면 하나로 정해서 관리하는 것이 효율적인 방식이다.

state를 묶어서 관리하는 단위를 component라고 한다.

## inverse data flow

state의 경우 부모에서 자식으로 top down 방식 전달이 일반적이다. 하지만 반대로 자식에 속한 form component에서 입력값 변경시 부모에 속한 state 값을 변경해야 하는 경우도 생긴다. 그럴 때는 자식에 함수를 정해줄 때 hook도 전달한다. hook은 자식 component에서 event 발생시에 변경하는 식으로 명시적으로 연결해준다

### 그러면 단계가 여러개일 경우 어떻게?

inline function이 쓰이는 경우? SRP를 위한

- 한번만 쓰는 경우 - 재사용할 여지 없을 때 호출 오버헤드를 제거한다.
- 나누기 애매할때 - SRP를 위해 굳이 나눠야할까 싶을 정도로 애매할 때.

## 기타

- golden record - 정리 필요
- inline function - 함수 호출 부분에 코드를 박아버린 함수. 호출시 발생하는 오버헤드가 없다.
- mock up 가짜 데이터

## reference
* [REST-wiki](https://ko.wikipedia.org/wiki/REST)
* [REST-NAVER d2](https://www.youtube.com/watch?v=RP_f5dMoHFc&t=9s)
1. [jsx 공식문서](https://facebook.github.io/jsx/)

- [inline-function](https://learn.microsoft.com/ko-kr/cpp/cpp/inline-functions-cpp?view=msvc-170)

## 학습 키워드

- REST API 와 GraphQL
  - REST API 란 무엇인가
  - GraphQL은 왜 등장했는가?
  - REST API vs GraphQL
- JSON
javascript 객체 표기법을 활용한 데이터 포맷, js 외에도 언어에 구애받지 않고 데이터를 주고 받을 때 표현방식으로 사용한다.
보낼때는 Stringify 해서 문자열로 만들어 전송에 용이하게 만들어 보낸다.
받은 이후에는 문자열 형태의 데이터를 parsing 해서 사용하기 좋게 JSON 객체 형식으로 변환한다. 직렬화 역직렬화와 유사하다는 생각이 든다.

- DSL(Domain-Specific Language) - 도메인 특화 언어
특정 도메인 풀기 쉽게 하기 위한 언어
html 과 유사한 DSL을 사용
- 선언형 프로그래밍 - 수행 대상에 대한 선언이나 함수호출을 하는 식을 다루는 프로그래밍 패러다임
- 명령형 프로그래밍 - 상태와 상태변경 위한 명령문을 순차수행하는 프로그래밍 패러다임
- SRP(단일 책임 원칙) - 모든 클래스는 각각 하나의 변경 원인,근거(책임)를 가지고, 그것을 캡슐화(속성 행위를 묶어서 외부에 보이지 않게 숨김)해야 한다.
React의 경우에는 component를 기준으로 해서 state를 가변적인 책임으로 삼아 캡슐화 한다.
css 도 class="asdf" 를통해 해당 클래스에 대한 내용을 넣어서 이미 쓰고 있다 .
information architecture - JSON schema의 영향 : 잘구조화되어있을 때 데이터 모델을 자연스럽게
- Atomic Design
- React component 와 props


## 학습 키워드

- REST API 와 GraphQL
    - REST API 란 무엇인가
    - GraphQL은 왜 등장했는가?
    - REST API vs GraphQL
- JSON
- DSL(Domain-Specific Language)
- 선언형 프로그래밍
- 명령형 프로그래밍
- SRP(단일 책임 원칙)
- Atomic Design
- React component 와 props
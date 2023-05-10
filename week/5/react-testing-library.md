# React Testing Library

## React Testing Library란?

[React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)는 DOM Testing library이다. react component(UI)에 대한 [테스트](https://www.robinwieruch.de/react-testing-library/)를 진행한다.

특징

* 사용자 관점에서 테스트를 하고 실제 DOM을 사용하기 때문에 브라우저에서의 상호작용을 확인할 수 있다.
* 함수, 객체들이 직관적으로 명명되어서 개발자 아닌 사람이 봐도 이해가 가능해서 소통에 유용하다.
* 연계 사용 : React 환경에서 Jest 같은 라이브러리와 같이 사용가능

## given - when - then 패턴

[GivenWhenThen](https://martinfowler.com/bliki/GivenWhenThen.html)은 테스트 시나리오 작성을 위한 구조화된 접근 방식이다. 이 방식으로 테스트를 구조화 하면 명확하고 일관되게 작성해서 이해하기 쉬워진다.

* GIVEN : 상황 / 전제 조건 - 초기 상태, 데이터를 준비
* WHEN : 테스트 하는 동작/이벤트를 수행
* THEN : 테스트 결과 검증 및 예상 결과를 명시한다.

[BDD testing](https://www.browserstack.com/guide/what-is-bdd-testing)

## BDD style?

Behavior Driven Development는 소프트웨어 동작 방식, 비즈니스 요구사항 - 동작 소프트웨어 간 상호작용을 강조하는 개발 방법론이다. BDD 에서는 Given-When-Then 구조로 시나리오를 작성하고, 요구사항과 프로그램 동작을 명확하게 정의한다.

BDD의 특징

* 요구사항 측(클라이언트) - 소프트웨어 측(개발자) 간 의사소통이 개선되고, 둘 간의 일치를 보장한다.
* 테스트 케이스의 문서화와 가독성, 유지보수성 향상을 보장한다.

[Behavior Driven Development - Introduction](https://www.tutorialspoint.com/behavior_driven_development/behavior_driven_development_introduction.htm)

## Mocking

실제 객체/함수 대신 Mock 객체로 대체 해서 의존성과 동작 결과를 예측가능하도록 제어한다.

Mock 객체는 실제 객체를 모방해서 원하는 결과반환 혹은 동작을 수행한다.

Mocking의 특징

* 외부 의존성 제어
* 테스트의 안정성 확보 및 일관성을 유지
* 복잡한 상황 재현, 특정 시나리오 테스트하기 용이

=> 테스트 케이스 작성 및 실행 속도 향상을 꾀할 수 있다.

Jest 에서 Mocking을 지원한다.

[Introduction to Mocking](https://www.codeproject.com/Articles/30381/Introduction-to-Mocking)
[Mock Testing](https://www.geeksforgeeks.org/software-testing-mock-testing/)

## Test fixture

테스트에서 사용되는 사전 설정된 상태나 환경이다.

* 테스트 실행 전에 필요한 환경(데이터, 객체, 설정)을 구성한다.
* 테스트 종료 후에는 해당 환경을 정리한다.

특징

* test fixture는 테스트의 독립성/일관성을 보장하고 실행의 신뢰성을 높일 수 있다.
* 테스트 케이스 간 공유데이터나 상태도 설정하는데 사용할 수 있다.

`setUp/beforeEach` 가 실행전에 호출 되고, 종료 후에는 `tearDown/afterEach`가 사용된다.

[test fixture](https://en.wikipedia.org/wiki/Test_fixture)

### beforeEach

테스트에서 context 부분에 이미 호출된 함수가 남아있는 것을 방지하기 위해 없애준다. 전체 context 부분에 적용되는 것이 일종의 횡단 관심사와 비슷한 컨셉.

반복 제거 : 함수 추출,

일종의 추상화를 통해 값의 비교를 아닌 호출의 여부를 비교해서 외부의 의존성을 줄인다. 의존성이 크면  mock 함수를 통해 조정해주면 나머지는 일괄 조정되기에 의존성 관리를 하기도 좋다.

swc는 type은 빼버린다. tsc --noEmit 할 시 compile 결과 없이 결과 검증을 할 수 있다.

mock에서 경로를 통한 함수 호출을 해준다.

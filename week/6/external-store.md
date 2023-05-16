
# External Store

external store - 외부 저장소

store가 react 내부에 있지 않음. useState로 관리하지 않음. react 가 관리하는 state는 (re)rendering에 관여되어 업데이트 하기 때문이다.

외부에서 상태정의를 했을 때는 eventHandler에서 처리해준다고해서 UI가 업데이트(rerendering) 되지 않는다. 그렇기에 강제 리렌더링이 필요하다. 그렇다면 외부에서 상태 정의를 왜 해줘야 하느냐는 의문이 생긴다. 거기에서 관심사의 분리가 나온다.

## 관심사의 분리

[Separation of Concerns](https://ko.wikipedia.org/wiki/%EA%B4%80%EC%8B%AC%EC%82%AC_%EB%B6%84%EB%A6%AC)

프로그램을 기준에 따라 작게 분리,격리하는 원칙.

관심사는 기능(장바구니 추가, 결제), 계층 등으로 구분이 가능하다. layered architecture 에서는 사용자와 얼마나 가까운지(UI/business logic/데이터)로 구분한다. 뭉뚱그려서 입력(Input) -> 처리(Process) -> 출력(Output)으로 나눌 수 있다. 프로그램은 보통 이 과정을 반복하는 구조이다.

MVC로 아래처럼 구분할 수도 있다.

```text
Model -> Process
View -> Output
Controller -> Input
```

관심사의 분리에서 각 관심사는 기능에 필요한 정보 이외에는 관심을 두지 않으며, 알 필요도 없다. 다른 모듈에는 캡슐화되어 인터페이스만 공개된다.

관심사를 분리하면 코드가 단순해지고, 단순해지면 유지보수성, 재사용성이 좋아진다.

> 프로그래밍 식 None of My Business, 소위 알빠노 이다

## Layered Architecture

[Layered Architecture - baeldung](https://www.baeldung.com/cs/layered-architecture)

[Multitier Architecture](https://en.wikipedia.org/wiki/Multitier_architecture)

[Layered Architecture - boostcourse](https://www.boostcourse.org/web316/lecture/16767?isDesc=false)

[layered architecture deep dive](https://msolo021015.medium.com/layered-architecture-deep-dive-c0a5f5a9aa37)

프로그램을 여러 계층으로 구성하는 아키텍처 스타일이며, [Multitier Architecture](https://en.wikipedia.org/wiki/Multitier_architecture) 으로도 불린다. Layer는 비슷한 역할을 하는 요소,코드들을 모아놓은 논리적인 구분이다.

### Three Tier Architecture

![3 tier](https://upload.wikimedia.org/wikipedia/commons/thumb/5/51/Overview_of_a_three-tier_application_vectorVersion.svg/1024px-Overview_of_a_three-tier_application_vectorVersion.svg.png)

* Presentation tier(UI, view): UI. 사용자 상호작용을 담당. 요청 작업과 결과를 해석하는 인터페이스 역할
* Logic tier : 데이터 처리, 비즈니스로직을 담당
* Data tier : 파일 시스템이나 DB에 담긴 정보를 담당

## Flux Architecture

[flux](https://facebookarchive.github.io/flux/)

[flux- in depth overview](https://facebookarchive.github.io/flux/docs/in-depth-overview) [한글](https://haruair.github.io/flux/docs/overview.html)

client-side application 만들때 사용하는 아키텍처 스타일

단방향 데이터 흐름(unidirectional data flow)을 통한 react view component 보완

MVC architecture가 가지고 있는 MODEL - VIEW 가 많아져서 생기는 복잡성(순환참조)을 해결하기 위한 대안이다.

![data flow](https://facebookarchive.github.io/flux/img/overview/flux-simple-f8-diagram-with-client-action-1300w.png)

action : 시스템에 들어오는 작업. view에서 사용자 상호작용에 의해 발생
dispatcher : 작업을 교통정리해서 (여러)store에 전달해준다. 중앙 허브 역할. 콜백을 store에 등록한다.
store : action에 따라 상태를 변경해준다.상태변경을 알려준다.
view : react component. 상태가 변하면 그에 따라 보이는 것들을 변경해준다. view에서 action이 발생되면 다시 dispatcher로 전파된다.

MVC의 2-way binding model view의 복잡한 관계를 단방향 data flow로 개선한다.

redux와의 차이점 - 단일 store를 사용한다

* store 에서 action 받고나서 reducer를 통해 state 변경한다.

> action 이 dispatch->store->view에 반영되고,해당결과로 또 action이 사이클을 돌기 때문에 흐름(flux) 이라 지은 것이다.

## Redux?

[Redux](https://ko.redux.js.org/tutorials/essentials/part-1-overview-concepts/)

Redux = Reduced + Flux (by Dan Abramov)

이벤트(action)을 이용해 application 상태를 전역적으로 관리/업데이트 하는 라이브러리/패턴. 단일 store, 단방향 data flow가 특징

![one way data flow](https://ko.redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)

사용 이유

* props drilling 해결
* state가 자주 변경될 때 사용
* update logic이 복잡할 때
* 어플리케이션 규모가 크고 협업이 필요할 때

### immutability

* 상태 업데이트는 기존 state에 대한 변경이 아닌 복제후 변경/추가하는 식으로 불변하게 진행된다.
* external store에서 상태를 그대로 세팅하면 rerendering을 안해주기에 별다른 연산이 없으면서도 강제 리렌더링을 해주도록 구조분해를 통한 객체 복사를 해줘야하는것이다.

### action

* type field가 존재하는 PJSO - metadata
* application의 변화를 의미하는 이벤트
* type 이외의 정보는 payload로 불린다 - real data

### action creator

* action 만들어서 객체로 돌려주는 함수

### useReducer

* state 와 action 객체를 받아서 기존 state를 변경하지 않고 새로운 state를 return 하는 함수
* action type에 따라 그에 맞는 작업을 수행하는 event listener
* 본래 reduce()는 사용자 정의 reducer function을 통해 이전까지의 연산결과와 현재 요소와의 연산을 통해 하나의 결과로 치환 된다. reducer가 명명 이유는 연산에 쓰이는 사용자 정의 reducer와 state 변경에 쓰이는 사용자 정의 reducer가 비슷해서이다.

입력 - 처리 - 출력으로 구분하자면 다음과 같다

* input - action + dispactch
* process - reducter
* output - view ( react)

### usecallBack()

매번 바뀌는 함수가 아닌, 계속 유지되는 함수를 사용할 때 useCallback을 사용한다. 항상 같아야 나중에 처리할 때 변경을 감지하도록 useEffect 의존성 배열에 걸어줄 수 있다.

왜 분리하는가? 앞에서 말했듯 UI / 비즈니스간 관심사의 분리를 적용해서 복잡도를 낮추도록 한다. BUSIness logic의 경우 분리가 안되면 UI 변화를 통해 검사해야하지만 분리한다면 신경쓸것 필요없이 test를 적용할 수 있어 테스트 작성시에도 용이하다. 공학적인 접근에는 알빠노주의가 선호된다


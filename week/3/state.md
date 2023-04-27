# State

## React UI 구성 방법

React UI를 구성할 때 5단계를 거친다. 마지막 3 단계는

3. 상황별 UI를 모두 보여주는 최소한의 UI State 설정
4. state를 관리하는 component 주체를 정한다.
5. 하위 -> 상위 컴포넌트 방향으로 state 변경사항을 전달하는 inverse data flow를 추가한다

## DRY 원칙

Don't repeat yourself - 복사 붙여넣기 하지 말기

### SSOT

데이터는 딱 한곳에서 제어, 조작하는 정보모델이 SSOT(Single Source of Truth) 이다. 현실세계에서 국민의 의료정보를 한곳에서 통합관리하고 각 병원에서 이걸 참조하는 사례도 이 모델에 해당한다.

State도 마찬가지다. 같은 state를 여러 군데에서 독자적으로 중구난방 사용하면 관리가 제대로 안된다. 만약 독자적인 state가 있고 이것을 모두 동기화 해준다면 일일이 업데이트를 해줘야 하니 state를 이용하는 과정보다 state 동기화 하는 과정이 더 많이 걸리게 될 수도 있다. 그렇게 보면 하나로 정해서 관리하는 것이 효율적인 방식이다.

## State 란?

한 화면 UI를 나눈 조각이 Component라면, Component는 특정 상태에 따라 표시하는 부분이 달라질 수 있다. component의 변화를 결정하는 가변적인 상태를 React의 State이다.

일관성 및 효율을 위해 DRY 원칙을 따르는 SSOT를 만들기. 중복을 지양하는 state를 만들기.

원칙을 따랐을 때 state가 아닌것

* 불변하는 것 - 상태가 가변적인 것을 상정하는데 불변하면 Nonsense
* props 통해 부모 component에게서 전달됨 - 그럼 props이지 state 아님.
* state/ props로 계산 가능 - '최소한의 정의'를 위반함

## useState

component에 state variable과 set function을 추가하는 react hook 이다.

```typescript
const [state, setState] = useState(initialState);
```

## 1급 객체

javascript에서 함수는 first-class object로 객체취급을 받으며, 함수 자체를 함수의 인자로 쓸수 있고, 함수 객체를 return 값으로 사용할 수 있다.

그렇기에 component 분리를 할 때 자식 component에서 상위에서 초기화된 setState에 접근할 필요가 생긴다. 상위 component 에서 하위 component로  props를 내려 보낼 수 있는데, javascript의 함수가 1급 객체 이기에 props로 setState를 내려보낼 수 있는 것이다. 익명함수, 클로저와 궁합이 좋아서 같이 쓰면 시너지 효과가 난다.

## Lifting State Up

state를 component 하나만 쓰는 경우도 있지만, 여러곳에서 쓰이는 경우도 있다. 그런 경우에는 state를 state 사용하는 component들의 공통 조상까지 끌어올리는 lift up 작업이 필요하다. DRY 원칙에 따른 SSOT 인 상태로 state를 만들기에 하나로 만들어야 한다. 그렇게 올리면 해당 부모가 state를 소유한다/책임진다.

## inverse data flow

state의 경우 부모에서 자식으로 top down 방식 전달이 일반적이다. 하지만 반대로 자식에 속한 form component에서 입력값 변경시 부모에 속한 state 값을 변경해야 하는 경우도 생긴다. 그럴 때는 자식에 함수를 정해줄 때 hook도 전달한다. hook은 자식 component에서 event 발생시에 변경하는 식으로 명시적으로 연결해준다. 이런 것을 콜백 함수라고 부른다.

## 기타

* golden record


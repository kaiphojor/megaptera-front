# 학습 키워드

## useRef

[`useRef`](https://react.dev/reference/react/useRef). 컴포넌트와 생명주기를 같이하는 쭉 동일한 객체. 바뀌더라도 상태처럼 리렌더링 되거나 하지는 않는다. 컴포넌트가 없어질때까지 참조할 수 있어야 하는 경우 쓰인다. 예를 들면 input을 여러개 생성할 경우에 그 ID를 관리해야하는경우 랜덤으로 useRef로 사용한다

객체라고 언급한 것은 참조객체로 접근한다는 점이다. 값을 직접 쓰지 않고, 객체의 current key값으로 접근해서 사용한다. state와는 다르게 current key값은 수정 가능하다. 하지만 state와 조금이라도 관련이 생기면 변경하면 안된다.

```typescript
import { useRef } from 'react';

function MyComponent() {
  const intervalRef = useRef(0);
  const inputRef = useRef(null);
  // ...
```

```text
const ref = useRef(Math.random());
id = {ref.current}
```

## Hook의 규칙

[규칙](https://ko.legacy.reactjs.org/docs/hooks-rules.html)

### 1. component 내 최상단에서 쓰여야 한다

반복문 / 조건문 / 중첩 함수 내에서 호출 하면 안된다. 항상 함수 최상위에서만 호출을 해야 렌더링시에 같은 순서로 hook 호출 되는 것이 보장된다.

state 와 useState 어떻게 상응하는지는 hook 호출 순서에 의존한다. 그러므로 hook 호출 순서가 복수가 되거나 조건부로 되어서 꼬여버리는 경우에는 제대로 동작하는 것을 보장 할 수 없다. 중첩 함수에서는 내 예상으로는 접근해서 처리해야하는 것들에 제대로 접근하지 못하는 경우가 발생할 수 있으므로 금지하는 것처럼 보인다.

### 2. component 나 custom hook 에서만 쓰여야 한다

이말은 즉슨 커스텀 훅와 외부 함수와의 차이점은 built-in hook을 쓰느냐의 여부인 것이었다. component 내 hook 호출, custom hook 내 hook 호출만 가능하다.

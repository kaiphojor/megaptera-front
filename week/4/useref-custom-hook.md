# 학습 키워드

- useRef

컴포넌트와 생명주기를 같이하는 쭉 동일하게 유지되는 객체. 바뀌더라도 상태처럼 리렌더링 되거나 하지는 않는다.
컴포넌트가 없어질때까지 같은 값이어야 하는 경우 쓰인다. 예를 들면 input을 여러개 생성할 경우에 그 ID를 관리해야하는경우 랜덤으로 useRef로 사용한다

```text
const ref = useRef(Math.random());
id = {ref.current}
```

커스텀 훅

훅을 감싸서 커스텀 훅을 만든다.

재사용할 여지도 만들고,

- Hook의 규칙

1. component 내 최상단에서 쓰여야 한다.
2. component 나 custom hook 에서만 쓰여야 한다.

이말은 즉슨 커스텀 훅와 외부 함수와의 차이점은 built-in hook을 쓰느냐의 여부인 것이었다

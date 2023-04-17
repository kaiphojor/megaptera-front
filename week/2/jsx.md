# JSX

## jsx란?

ECMAcript 의 XML 식 구문 확장판.
xml 처럼 비슷하며 js 내에서 쓰인다.
html을 포함한 xml 식 코드를 Javascript 코드로 1대1 변환을 해준다.

쓰는 이유는 html을 js에서 react.createElement 같은거 없이 보이는 그대로 직관적으로 편하게 쓸수 있기 때문이다.

syntactic sugar는 구문적으로 편하게 쓸 수 있는 방법 인것 같다

react.createElement는 react 에서 html element를 만드는 메소드이다. jsx 없이 react에서 element 작성시 필수인것 같 다.

react strict mode는 react에 엄청 엄격한 규칙을 적용하는 방법인것 같다.

VDOM은 virtual dom 으로 front end framework 에서 사용한다. DOM 대신 VDOM을 사용한다. html css js 프레임워크 없는 구조에서는 DOM을 직접 조작하지만, framework 사용시 DOM을 virtual DOM으로 간접 조작한다. vdom을 중간에 두면 이점이 있는데 모르겠다.
VDOM은 virtual DOM인데 DOM은 하나 변경시 모든게 업데이트 되지만 VDOM은 해당 부분과 하위 부분만 업데이트 된다.

Reconciliation (재조정) 뭔가 화면 업데이트 관련해서 재조정을 수행한다는 것 같다.

## 학습 키워드

- React에서 JSX를 사용하는 목적
- Syntactic sugar
- React.createElement
- React Element
- React StrictMode
- VDOM(Virtual DOM)이란?
    - DOM이란?
    - DOM과 Virtual DOM의 차이
- Reconciliation(재조정) 과정은 무엇인가?
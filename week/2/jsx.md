# JSX

## JSX란?

JavaScript 파일에서 쓰이는 XML류의 문법 확장이고 전처리기 처리 시 정식 JS 코드로 변환된다. attribute 붙은 tree 구조를 xml 비슷한 식으로 간결하고 친숙하게 정의 하는 것이 원래 목적이다.

### jsx가 왜 만들어졌는가?

웹 구성 시에 html, js 파일이 분리되어 있는경우가 많았었다. 하지만 상호작용성이 더 커지면서 로직이 UI 컨텐츠를 결정하는 경우가 많아졌다. 마크업과 js를 함께 관리하면 한곳에 모여있어 유지보수, 수정시 편하다. react에선 마크업과 js코드가 합쳐진 component 단위가 있다. 해당 마크업을 js 파일에서 표현하기 위해 JSX가 고안되게 되었다.

### react에서의 쓰임

React에서는 JSX를 통해 element를 트리 구조로 보기 쉽게 표현할 수 있다. 이는 javascript 코드 내에서 UI 작업을 편리하게 할 수 있다. 그리고 JSX 표현식 형태는 마크업과 JS 코드의 혼종이지만 컴파일 이후에는 엄연한 JS 함수, 객체로 변환된다.

### React의 element란?

React application에서 화면을 그려주는 최소 구성 단위. 일반 객체로 받아들여진다. ReactDOM에서 root DOM 노드를 등록한뒤, root DOMnode 밑에 DOM element를 등록한다. ReactDOM은 등록된 모든 element들을 관리하며 그것들의 정보를 DOM에 업데이트한다.

### jsx 와 jsp

JSX는 코드 삽입 면에서는 JSP하고 반대이다. 갑자기 java이야기이지만 jsp가 html 내 java코드를 삽입할 수 있게 만든 것이라면 JSX는 js 코드내 마크업을 삽입하기 위한 문법의 확장이다. 하지만 변환이 모두 코드로 된다는 점은 동일하다. JSP는 servlet Java/class 파일로 바뀌고, JSX 도 결국 js 코드에 1대1로 js 함수화, 객체화 변환되어 js 파일에 녹아들기 때문이다. 그리고 이 둘이 UI를 각각 java/js 로직으로 그려낸다는 점에서 비슷한 것 같다.

### jsx없이 마크업 생성

JSX 코드는 `<p>Hello, world!</p>` 라고 할 때 해당 코드는 js 코드로 `React.createElement("p", null, "Hello, world!");` 로 변환 된다. 태그 하나에 `React.createElement` 하나가 대응된다.

js 코드를 직접 쓰면 JSX 코드는 필요없다. 하지만, 그렇게 해서는 JSX 코드로 보면 간단히 파악할 수 있는 트리 구조를 일일이 떠올려가며 작업해야한다. 또한 위 예시는 간편해서 그렇지 조금만 복잡해져도 귀찮아진다.

자세한 사항은 reference 참고

### syntactic sugar

syntactic sugar는 코드를 더 이해하고 읽고 쓰기 편하게 만들어주는 구문(문법)이다. 똑같은 기능이어도 간략화되고, 이해가 쉬워서 유지보수하기에 도움이 된다.

```jsx
<div className="test">
    <p>Hello, world!</p>
    <Button type="submit">Send</Button>
</div>
```

위 JSX 코드를 변환하면 아래처럼 나온다. JSX쪽이 한눈에 파악이 되고 아래는 `React.createElement` 안쪽에 중첩이 되어 보기 불편하다. tab으로 그나마 보기 편하게 만들었지만 보기 쉽게 만들기 위해 저런 수고를 다해야 한다는 것은 원래 보기 어렵다는 방증이다.

```javascript
React.createElement(
    "div",
    { className: "test" },
    React.createElement("p", null, "Hello, world!"),
    React.createElement(Button, { type: "submit" }, "Send")
);
```

### StrictMode

적용 범위 컴포넌트 내의 요소에 불완전 rendering,  effect 정리 누락 , deprecated API 사용등의 버그를 검사해서 경고해주는 컴포넌트이다. 검사를 하기위해 StrictMode는 추가시간을 들여서 re-rendering 을 하거나 effect를 다시 실행하거나 한다.

고로, 초기 개발시에 버그 잡는 용으로만 임시로 쓰기에 좋다. 왜냐하면 해당 component는 버그를 탐지해내기 위해 일부러 추가시간을 들여서 re-rendering을 하고, effect를 다시 수행하기 때문에 배포시에는 오히려 방해가 되기 때문이다. 따라서 배포 이전까지 문제점을 해결하고 component를 제거하는 것이 맞다.

적용하는이게 뭔가. 왜 쓰이는가? 쓰면 이점이 뭔가?
뭔가 엄격한 룰을 적용해서 제한을 거는 모드인것같다. 그리고 제약에 대한 tradeoff로 얻는 것이 있을 것이다.

#### StrictMode의 사용법

적용시에는 Component
import 후 모드적용할 범위를 태그 여닫는 범위로 정한다.

```javascript
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```



그리고
규칙
속성
문자열 리터럴 - 따옴표
attribute 내 JS 표현식 - 중괄호. camelCase (중괄호 주변 따옴표 사용 금지)

escape - URI로 전달 위한 문자열 인코딩 - https://opentutorials.org/course/50/191

facebook에서 2013년에 react library에서의 사용을 위해 만들었다.

추가 - ECMAscript란? 관심사의 분리
https://en.wikipedia.org/wiki/Separation_of_concerns

syntactic sugar는 구문적으로 편하게 쓸 수 있는 방법 인것 같다

react.createElement는 react 에서 html element를 만드는 메소드이다. jsx 없이 react에서 element 작성시 필수인것 같 다.

react strict mode는 react에 엄청 엄격한 규칙을 적용하는 방법인것 같다.

VDOM은 virtual dom 으로 front end framework 에서 사용한다. DOM 대신 VDOM을 사용한다. html css js 프레임워크 없는 구조에서는 DOM을 직접 조작하지만, framework 사용시 DOM을 virtual DOM으로 간접 조작한다. vdom을 중간에 두면 이점이 있는데 모르겠다.
VDOM은 virtual DOM인데 DOM은 하나 변경시 모든게 업데이트 되지만 VDOM은 해당 부분과 하위 부분만 업데이트 된다.
VDOM은 관리와 유지보수 측면
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

## reference

1. [jsx 공식문서](https://facebook.github.io/jsx/)
2. [react-jsx](https://react.dev/learn/writing-markup-with-jsx#jsx-putting-markup-into-javascript)
3. [strictMode](https://react.dev/reference/react/StrictMode#strictmode)
4. [jsx 없이 element 만들기](https://react.dev/reference/react/createElement#creating-an-element-without-jsx)
5. [element-rendering](https://ko.reactjs.org/docs/rendering-elements.html)
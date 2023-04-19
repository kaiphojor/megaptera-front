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

## Component란?

재사용 가능한 UI 조각이고, props 속성 데이터를 인자로 받아서 React element를 반환한다. `React.component` 혹은 function을 통해 정의한다. 요즘은 function component 정의를 추천한다.

여기까지만 보면 React application을 구성하는 요소인 element와 뭐가 다른지 구분이 안간다. 그저 component가 element의 상위에 있다는 차이일뿐. 하지만 Component는 다른 component를 조합해서 생성 할 수 있다는 점이 있다. 이걸 component의 합성이라 한다. element는 여러 element를 합성해서 element를 만드는 기능이없다. 이와 반대로 큰 component를 여러개의 작은 component로 분리하는 작업을 component 추출이라 한다.

## StrictMode

적용 범위 컴포넌트 내의 요소에 불완전 rendering,  effect 정리 누락 , deprecated API 사용등의 버그를 검사해서 경고해주는 내장 컴포넌트이다. 검사를 하기위해 StrictMode는 추가시간을 들여서 re-rendering 을 하거나 effect를 다시 실행하거나 한다.

고로, 초기 개발시에 버그 잡는 용으로만 임시로 쓰기에 좋다. 왜냐하면 해당 component는 버그를 탐지해내기 위해 일부러 추가시간을 들여서 re-rendering을 하고, effect를 다시 수행하기 때문에 배포시에는 오히려 방해가 되기 때문이다. 따라서 배포 이전까지 문제점을 해결하고 component를 제거하는 것이 맞다.

### StrictMode의 사용법

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

## DOM이란?

Document Object Model. 문서 객체 모델로 HTML/XML 문서에 대한 programming  interface 이다. Document에는 page content가 저장되어 있고 Javascript로 접근해서 조작이 가능하다. Document는 Node들이 모인 tree 형태로 표현 되어있기에 DOM Tree 라고 한다. API(web/xml)는 뭉뚱그려 말하자면 DOM과 script 언어의 조합이다.

dom interface에서 주요 object는 브라우저를 뜻하는 `window` 와 root document를 가리키는 `Document`가 있다. `Node` interface 에서 상속받은 `Node` 와 `Element` 가 있고, `Element` interface 또한 있다.

## VDOM(Virtual DOM)이란?

메모리 상에 존재하는 가상의 React Element Tree. 가상의 element Tree의 업데이트 시 ReactDOM library를 통해 실제 UI인 DOM Tree 에 반영 하는 표현 방식. element Tree의 변경된 부분만 찾아서 바꾸는 과정을 재조정(Reconciliation)이라고 함.

### Reconciliation(재조정) 과정은 무엇인가?

새로운 element Tree 생성을 할때 두 가정을 기반으로 O(n) 복잡도의 휴리스틱 알고리즘을 적용해서 더욱 빠르게 렌더링을 한다.

1. type 이 다른 element는 다른 tree를 생성
2. key prop을 통해 변경하지 말아야 하는 자식 엘리먼트를 표시할 수 있다.

추가로 같은 타입의 element에 대해서도 속성이 다르면 같은 부분은 놔두고 다른 부분만 갱신한다.
element tree는 자식도 tree이기에 root에서부터 재귀적으로 갱신처리를 한다. 그 경우 list에 key attribute를 지원해서 변경 없는 자식에 대한 표식을 남긴다. 만약 key가 없을경우 리스트를 순회할 때 끝에 추가되는 경우엔 트리의 변경은 순조롭다. 하지만 앞에 element를 끼워 넣는 경우엔 diffing이 꼬여서 변경사항이 아닌것도 갱신 해버리게 된다. 그렇기 때문에 key를 넣어서 비 갱신 자식 element를 명확하게 하는 것이다.

### DOM과 Virtual DOM의 차이

UI 업데이트 시 DOM을 직접 변경하는 것과는 달리 Virtual DOM에서는 메모리상의 element Tree를 변경사항을 갱신하고, 그 후에 DOM에 반영 한다.

또한 VDOM은 이전 element tree 와의 비교(diffing)를 해서 최소한의 변경사항만 렌더링 하기 때문에 좀 더 효율적인 DOM 조작/렌더링이 가능하다. 하지만 적당히 빠르지 중요한 것은 유지보수성의 향상이다.

DOM tree를 일일이 조작하는 것보다 react element를 변경하는 작업은 tree 구조, 변경사항을 눈으로 바로 확인할 수 있어 직관적이고 편하다. 이러한 편의성은 많은 양의 작업을 한다고 가정할 때 유지보수성의 증가로 이어진다.

### VDOM과 선언적 API?

이는 재조정과 virtual DOM 에서 나오며 react의 virtual DOM 방식이 React의 선언적 API를 가능하게 한다. 선언적 API를 통해 '선언'만 하면 나머지 내부 동작은 신경쓰지 않아도 되는 정도로 추상화가 된다.

휴리스틱 알고리즘 - 최적해를 찾지 못하거나 시간이 너무 걸릴 때 실용적인 방법을 도입해서 근사해를 구하는 접근법. 보통 경험칙, 시행착오, 상식적인 전략, 직관을 사용하여 문제를 해결한다. 이 접근법의 특징은 정확성을 희생해서 문제 해결 속도를 높이는 편이다.

escape - URI로 전달 위한 문자열 인코딩 - https://opentutorials.org/course/50/191

facebook에서 2013년에 react library에서의 사용을 위해 만들었다.

추가 - ECMAscript란? 관심사의 분리
https://en.wikipedia.org/wiki/Separation_of_concerns

## reference

1. [jsx 공식문서](https://facebook.github.io/jsx/)
2. [react-jsx](https://react.dev/learn/writing-markup-with-jsx#jsx-putting-markup-into-javascript)
3. [jsx-depth](https://ko.reactjs.org/docs/jsx-in-depth.html)
4. [strictMode](https://react.dev/reference/react/StrictMode#strictmode)
5. [jsx 없이 element 만들기](https://react.dev/reference/react/createElement#creating-an-element-without-jsx)
6. [element-rendering](https://ko.reactjs.org/docs/rendering-elements.html)
7. [Component](https://ko.reactjs.org/docs/components-and-props.html)
8. [DOM](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction)
9. [DOM(2)](https://developer.mozilla.org/ko/docs/Glossary/DOM)
10. [Virtual DOM](https://ko.reactjs.org/docs/faq-internals.html#what-is-the-virtual-dom)
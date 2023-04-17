# JSX

## JSX란?

JavaScript 파일에서 쓰이는 ECMAscript 의 XML류 문법 확장. 그러나 ECMAscript 사양에 포함하진 않는다. 전처리기(transpiler)에 의해 정식 JS 코드로 변환됨. attribute 붙은 tree 구조를 xml 비슷한 식으로 간결하고 친숙하게 정의 하는 것이 원래 목적이다.

react에서의 쓰임
React에서는 JSX를 통해 element를 트리 구조로 보기 쉽게 표현할 수 있다. 이는 javascript 코드 내에서 UI 작업을 편리하게 할 수 있다. 그리고 JSX 표현식 형태는 마크업과 JS 코드의 혼종이지만 컴파일 이후에는 엄연한 JS 함수, 객체로 변환된다.

jsx가 왜 필요하게 되었는가?
웹 구성 시에 html, js 파일이 분리되어 있는경우가 많았었다. 하지만 상호작용성이 더 커지면서 로직이 UI 컨텐츠를 결정하는 경우가 많아졌다. 그렇게 마크업과 js코드가 합쳐진 component가 생겨나게 되었고 마크업을 js 파일에서 표현하기 위해 JSX가 고안되게 되었다.

JSX는 코드 삽입 면에서는 JSP하고 반대이다. 갑자기 java이야기이지만 jsp가 html 내 java코드를 삽입할 수 있게 만든 것이라면 JSX는 js 코드내 html을 포함한 xml 코드를 삽입하기 위한 문법의 확장이다. 하지만 변환이 모두 코드로 된다는 점은 동일하다. JSP는 servlet Java/class 파일로 바뀌고, JSX 도 결국 js 코드에 1대1로 js 함수화, 객체화 변환되어 js 파일에 녹아들기 때문이다. 그리고 이 둘이 UI를 각각 java/js 로직으로 그려낸다는 점에서 비슷하다는 쪽에 무게를 더 두고 싶다.


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

# CSS in JS

javascript 안에서 Style Component 사용해서 css 사용하는 것

## CSS in JS 란

[CSS-in-JS(Wiki)](https://en.wikipedia.org/wiki/CSS-in-JS)

JS를 사용해서 style component를 구성하는 style technique

component 단위로 css를 사용할 수 있다.

성능상의 이슈가 있다 .

implementation(기술의 구현체)의 종류

* Styled Components - 실습에 적용할 라이브러리
* [JSS](https://cssinjs.org/?v=v10.10.0)
* [Tailwind CSS](https://en.wikipedia.org/wiki/Tailwind_CSS)

구현체 특징

* 선언적
* 재사용성
* 프레임워크에 종속적이지 않음

> agnostic : 무신론적인, 중립적인 --> 특정 ~에 종속적이지 않음(프로그래밍)

## CSS

[CSS](https://developer.mozilla.org/ko/docs/Web/CSS)

cascading style sheet는 html 문서의 표현방법을 선언적으로 기술한 언어.

규칙 기반 언어

### 선택자

rule set을 적용할 범위를 지정하는 방법

[선택자의 종류](https://developer.mozilla.org/ko/docs/Learn/Getting_started_with_the_web/CSS_basics#%EC%84%A0%ED%83%9D%EC%9E%90%EC%9D%98_%EC%97%AC%EB%9F%AC_%EC%A2%85%EB%A5%98)

* 요소 타입 - `p`
* id - `#id`
* class - `.class`
* 속성 - `img[src]`
* pseudo class - `a:hover`

### 미디어 쿼리

[미디어 쿼리](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_media_queries)

기기별, 파라미터 별 조정하는 방법. 반응형 디자인의 핵심요소

### Box Model

[box model](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/The_box_model)

유형

* 블록 박스  - 개행 O, width/height 속성 고려, 패딩/여백/테두리로 다른요소 밀어내기
* 인라인 박스 - 개행 X

그 외

* [CSS-MDN](https://developer.mozilla.org/ko/docs/Web/CSS/Reference)
* [flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
* [Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

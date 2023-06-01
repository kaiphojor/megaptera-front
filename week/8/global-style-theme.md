# Global Style & Theme

## Reset CSS

기본적으로 적용되어있는 css 속성들을 싹 지워준다.

## `box-sizing` 속성

[box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)

요소의 크기를 주변 계층 관계 관련해서 어떻게 조정할지에 대한 설정

## `word-break` 속성

[word break](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break)

text가 box 범위를 넘을때 어떻게 처리할지에 대한 설정

## Theme

다크모드 지원시 필요. 다크 모드를 잘 정의하고 의미에 집중하게 됨

+ 의미에 집중한다. 단순히 빨간색, 하얀색 이라고 하면 해당 테마에서 어떤 '의미'를 가지는지 알 수 없다.

색깔 자체의 의미(단편적인 의미)도 있지만, 특정 색이 해당 테마에서 어떤 요소로 기능하고 있는지 ( 배경색인가? 주 색인가? 글자 색인가?) 그리고 해당 맥락에서의 의미를 뜻한다.

## ThemeProvider

[styled-component: theming](https://styled-components.com/docs/advanced#theming)

테마 관리용 component. 전역적인 테마 설정 및 다른 component에 테마 속성 전달.

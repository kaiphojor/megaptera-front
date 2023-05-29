# Design System

디자인 시스템

API 같기도 하고, 코딩스타일 비슷해보이기도 한다.

## 반응형 웹 디자인(Responsive web design)

[Design System - Laura Kalbag](https://24ways.org/2012/design-systems/)

[Design System Slide - Laura Kalbag](https://speakerdeck.com/laurakalbag/design-systems-1)

디자인 패러다임의 변화

* 웹 -> 모바일 -> 그 외 다양한 장비 지원(다양한 viewports)
* 레이아웃 : 고정 너비 -> 가변 너비

> viewport - 웹 페이지의 가시적인 영역

디자인 시스템의 요소

고정 요소 - **컨텐츠**, 서체, 색깔, 모양(shape/form), 기본 단위
가변 요소 - 그리드(테이블), 레이아웃, 글자크기, 글 가로/세로 폭(measure, leading)

어떤 장비로 웹에 접근할지 모르기에 유동적으로 컨텐츠를 보여준다.

## 디자인 시스템(Design System)

[Design Systems 101 - Therese Fessenden](https://www.nngroup.com/articles/design-systems-101/)

> Definition: A design system is a complete set of standards intended to manage design at scale using reusable components and patterns.

* 재사용 가능한 components/patterns
* 대규모로 디자인을 관리
* 표준 집합

사용하는 이유

* 재사용성
* (시각적) 일관성 - UI components/elements를 재사용하면서 일관성도 달성된다
* 더 중요한 문제에 집중 - 재사용으로 인해 복붙하는 부분에는 신경 안써도 됨. 일종의 관심사의 분리
* 소통의 원활 - 통일된 기준(언어)를 사용하면서 소통 비용이 감소됨

사용하기 어려울 때

* 시간이 촉박할 때 - 적용에 시간이 걸림, 사용법 익히는데 시간이 걸림.
* 한번 쓰고 말 때 - 사용의 의미가 없음

회사별 디자인 시스템

* [Atlassian Design System](https://atlassian.design/)
* [Material Design (Google)](https://material.io/)
* [Base Web (Uber)](https://baseweb.design/)
* [Polaris (Shopify)](https://polaris.shopify.com/)
* [Lightning Design System (Salesforce)](https://www.lightningdesignsystem.com/)
* [Mailchimp Pattern Library](https://ux.mailchimp.com/patterns)
* [Ant Design](https://ant.design/)

UX reference

* [제이콥 닐슨](https://ko.wikipedia.org/wiki/제이콥_닐슨)
* [도널드 노먼](https://ko.wikipedia.org/wiki/도널드_노먼)
* [앨런 쿠퍼](https://en.wikipedia.org/wiki/Alan_Cooper)

실제 적용시에는 Theme과 Component를 활용할 수 있다.

## Atomic Design

Design System을 만들기 위한 방법론. component 분리 부분에서 이미 언급이 되었었다.

* [Atomic Design 소개 글](https://bradfrost.com/blog/post/atomic-web-design/)
* [Atomic Design 전자책](https://atomicdesign.bradfrost.com/)
